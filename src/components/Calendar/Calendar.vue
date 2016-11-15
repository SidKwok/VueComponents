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
export default {
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
                    case 'resend':
                        this.resendDailyReport(
                            this.combineDate(new Date(this.currentDate - 24 * 60 * 60 * 1000))
                        );
                        break;
                    default:
                        break;
                }
            }
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
    .daily-report {
        width: 100%;
        height: 792px;
    }
    .daily-report .header {
        font-size: 30px;
        height: 54px;
        border-bottom: 1px solid #ddd;
    }
    .daily-report .header .year,
    .daily-report .header .month {
        display: inline-block;
        position: relative;
    }
    .daily-report .header .year i,
    .daily-report .header .month i {
        top: -5px;
        position: relative;
        font-size: .5em;
        color: #ddd;
    }
    .daily-report .header .year ul,
    .daily-report .header .month ul {
        position: absolute;
        top: 36px;
        width: 112px;
        height: auto;
        background-color: #fff;
        padding: 8px 0px;
        box-shadow: 0px 0px 10px 0px rgba(0,0,0,0.2);
        z-index: 1;
        display: none;
    }
    .daily-report .header .year ul li,
    .daily-report .header .month ul li {
        height: 32px;
        font-size: 14px;
        padding-left: 16px;
        line-height: 32px;
        cursor: pointer;
    }
    .daily-report .header .year ul li:hover,
    .daily-report .header .month ul li:hover {
        background-color: #ebf5fd;
    }
    .daily-report .header .year ul .active,
    .daily-report .header .month ul .active {
        color: #008cff;
    }
    .daily-report .header .year:focus > ul,
    .daily-report .header .month:focus > ul {
        display: block;
    }
    .daily-report .header .year:focus > i,
    .daily-report .header .month:focus > i {
        transform: rotate(180deg);
    }
    .daily-report .header .resend,
    .daily-report .header .config {
        float: right;
        font-size: 14px;
        color: #008cff;
        margin-left: 48px;
    }
    .daily-report .header a:nth-child(2) {
        margin-left: 24px;
    }
    .daily-report .calendar {
        width: 100%;
    }
    .daily-report .calendar .row {
        display: flex;
        justify-content: space-between;
    }
    .daily-report .calendar .row .week-header {
        height: 56px;
        flex: 1;
        border-bottom: 1px solid #ddd;
        line-height: 56px;
        font-size: 14px;
        padding-left: 16px;
        font-weight: 500;
    }
    .daily-report .calendar .row .day {
        flex: 1;
        display: inline-block;
        height: 136px;
        border: 1px solid #ddd;
        border-left: none;
        border-top: none;
        font-size: 16px;
        padding: 16px;
    }
    .daily-report .calendar .row .day:nth-child(1) {
        border-left: 1px solid #ddd;
    }
    .daily-report .calendar .row .gray {
        color: #ddd;
        pointer-events: none;
        cursor: no-drop;
    }
    .daily-report .calendar .row .active {
        background-color: #e5f3ff;
    }
</style>
