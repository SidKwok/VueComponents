<template lang="html">
    <input type="text" v-model="test" v-el:datepicker>
</template>

<script>
    import Flatpickr from 'flatpickr';

    /**
     * init Flatpickr with particular languange
     * @param {String} lang - language
     */
    const chooseLang = lang => {
        switch (lang) {
            case 'zh':
                Flatpickr.init.prototype.l10n.weekdays = {
                    shorthand: ['周日', '周一', '周二', '周三', '周四', '周五', '周六'],
                    longhand: ['星期日', '星期一', '星期二', '星期三', '星期四', '星期五', '星期六']
                };

                Flatpickr.init.prototype.l10n.months = {
                    shorthand: ['一月', '二月', '三月', '四月', '五月', '六月', '七月', '八月', '九月', '十月', '十一月', '十二月'],
                    longhand: ['一月', '二月', '三月', '四月', '五月', '六月', '七月', '八月', '九月', '十月', '十一月', '十二月']
                };
                return;
                break;
            default:
                return;
        }
    }
    export default {
        data() {
            return {
                dp: null,
                test: ''
            }
        },
        props: {
            // you can check the documentation(https://chmln.github.io/flatpickr/)
            // to custom the options whatever you want
            // just don't mess up with onChange
            // coz i used it to update the date
            // i will find a better way to solve thi :-(
            options: {
                type: Object,
                default() {
                    return {};
                }
            },
            // send the date out
            // has to be twoWay binding
            // so it can pass the date out of the component
            date: {
                type: String,
                required: true,
                twoWay: true
            },
            // choose the particular language
            lang: {
                type: String,
                default: 'en'
            }
        },
        ready() {
            // we need a onChange event to pass the date outside
            let _this = this;
            let options = _this.options;
            chooseLang(_this.lang)
            options.onChange = (dateObj, dateStr) => _this.date = dateStr;
            this.dp = new Flatpickr(this.$els.datepicker, options);
        }
    };
</script>

<style lang="css">
    @import '../../../node_modules/flatpickr/dist/flatpickr.min.css';
</style>
