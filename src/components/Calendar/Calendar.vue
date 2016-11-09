<template lang="html">
    <div class="daily-report">
        <div class="header" @click="handleHeaderClick($event)">
            <a href="javascript: void(0);" class="year">
                {{ year }} 年 <i class="fa fa-angle-down"></i>
                <ul>
                    <li data-type="year" data-year="2013">2013 月</li>
                    <li data-type="year" data-year="2014">2014 月</li>
                    <li data-type="year" data-year="2015">2015 月</li>
                    <li data-type="year" data-year="2016">2016 月</li>
                    <li data-type="year" data-year="2017">2017 月</li>
                </ul>
            </a>
            <a href="javascript: void(0);" class="month">
                {{ month }} 月 <i class="fa fa-angle-down"></i>
                <ul>
                    <li data-type="month" data-month="1">1 月</li>
                    <li data-type="month" data-month="2">2 月</li>
                    <li data-type="month" data-month="3">3 月</li>
                    <li data-type="month" data-month="4">4 月</li>
                    <li data-type="month" data-month="5">5 月</li>
                    <li data-type="month" data-month="6">6 月</li>
                    <li data-type="month" data-month="7">7 月</li>
                    <li data-type="month" data-month="8">8 月</li>
                    <li data-type="month" data-month="9">9 月</li>
                    <li data-type="month" data-month="10">10 月</li>
                    <li data-type="month" data-month="11">11 月</li>
                    <li data-type="month" data-month="12">12 月</li>
                </ul>
            </a>
            <a href="javascript: void(0);" class="config" data-type="config">
                <i class="fa fa-gear"></i> 日报配置
            </a>
            <a href="javascript: void(0);" class="resend" data-type="resend">
                <i class="fa fa-rotate-left"></i> 重发前一封日报
            </a>
        </div>
        <div class="calendar" @click="getDailyReportContent($event)">
            <div class="row">
                <span class="week-header">Sunday</span>
                <span class="week-header">Monday</span>
                <span class="week-header">Tuesday</span>
                <span class="week-header">Wednesday</span>
                <span class="week-header">Thursday</span>
                <span class="week-header">Friday</span>
                <span class="week-header">Saturday</span>
            </div>
            <div class="row" v-for="row of calendar">
                <a href="javascript: void(0);" :data-date="combineDate(day)"
                    :class="['day', (day.getMonth() + 1) !== month ? 'gray' : '',
                            isEqual(day, currentDate) ? 'active' : '']"
                    v-for="day of row">
                    {{ day.getDate() | format }}
                </a>
            </div>
        </div>
    </div>
</template>

<script>
import routeMixin from 'mixins/routeMixin';
import { Get } from 'state/actions';
import { getAppInfo } from 'state/getters';
export default {
    head: {
        title: {
            inner: '日报'
        }
    },
    mixins: [routeMixin],
    data() {
        let currentDate = new Date();
        return {
            currentDate,
            year: currentDate.getFullYear(),
            month: currentDate.getMonth() + 1
        };
    },
    computed: {
        showDate() {
            let date = new Date();
            date.setUTCFullYear(this.year);
            date.setUTCMonth(this.month - 1);

            return date;
        },
        calendar() {
            const day = 24 * 60 * 60 * 1000;
            const currentDate = this.showDate;
            const currentDay = currentDate.getDate();
            const oneDate = new Date(currentDate - (currentDay - 1) * day);
            const oneWeekday = oneDate.getDay();
            const startDate = new Date(oneDate - (oneWeekday - 0) * day);

            let arr = [];
            let tmp = [];
            for (let i = 0; i < 35; i++) {
                tmp.push(new Date(Number(startDate) + i * day));
                if (!((i + 1) % 7)) {
                    arr.push(tmp);
                    tmp = [];
                }
            }

            // 最后一天的下一天
            let lastNextDay = new Date(Number(arr[4][6]) + day).getDate();
            if (lastNextDay > 29 && lastNextDay < 32) {
                tmp = [];
                for (let i = 0; i < 7; i++) {
                    tmp.push(new Date(Number(arr[4][6]) + i * day));
                }
                arr.push(tmp);
            }
            return arr;
        }
    },
    vuex: {
        actions: {
            Get
        },
        getters: {
            app: getAppInfo
        }
    },
    methods: {
        isEqual(day, currentDay) {
            return (day.getFullYear() === currentDay.getFullYear()
                && day.getMonth() === currentDay.getMonth()
                && day.getDate() === currentDay.getDate()
            );
        },
        combineDate(date) {
            const year = '' + date.getFullYear();
            const month = date.getMonth() + 1 + '';
            const day = '' + date.getDate();
            return year + (month.length === 2 ? month : '0' + month)
                + (day.length === 2 ? day : '0' + day);
        },
        handleHeaderClick(e) {
            const dataset = e.target.dataset;
            const type = e.target.dataset.type;
            if (type) {
                switch (type) {
                    case 'year':
                        this.year = Number(dataset.year);
                        e.target.parentNode.parentNode.blur();
                        break;
                    case 'month':
                        this.month = Number(dataset.month);
                        e.target.parentNode.parentNode.blur();
                        break;
                    case 'config':
                        // TODO
                        break;
                    case 'resend':
                        this.resendDailyReport(
                            this.combineDate(new Date(this.currentDate - 24 * 60 * 60 * 1000))
                        );
                        break;
                    default:
                        break;
                }
            }
        },
        getDailyReportContent(e) {
            const date = e.target.dataset.date;
            if (date) {
                this.Get(
                    '/daily-report/get-daily-report-content',
                    {
                        appKey: this.app.key,
                        date
                    }
                ).then(retData => {
                    console.log(retData);
                }).catch(err => console.log(err));
            }
        },
        resendDailyReport(date) {
            this.Get(
                '/daily-report/resend-daily-report',
                {
                    appKey: this.app.key,
                    date
                }
            ).then(retData => console.log(retData))
            .catch(errMsg => console.log(errMsg));
        }
    },
    filters: {
        format(val) {
            // 先转化为字符串
            let str = val + '';
            return (str.length === 2)
                ? str : '0' + str;
        }
    }
};
</script>

<style scoped>
</style>
