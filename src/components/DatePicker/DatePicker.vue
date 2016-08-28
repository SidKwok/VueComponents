<template lang="html">
    <input type="text" v-model="test" v-el:datepicker>
</template>

<script>
    import Flatpickr from 'flatpickr';
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
            }
        },
        watch: {
            test(val) {
                console.log(val)
            }
        },
        ready() {
            // we need a onChange event to pass the date outside
            let _this = this;
            let options = _this.options;
            options.onChange = (dateObj, dateStr) => _this.date = dateStr;
            this.dp = new Flatpickr(this.$els.datepicker, options);
        }
    };
</script>

<style lang="css">
    @import '../../../node_modules/flatpickr/dist/flatpickr.min.css';
</style>
