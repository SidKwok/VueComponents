<template lang="html">
    <div class="chart" v-el:chart
        :style="{
            width: `${width}px`,
            height: `${height}px`
            }"
    ></div>
</template>

<script>
    import Echarts from 'echarts';
    export default {
        props: {
            // a chart object that can be used outside
            // you can do the event outside the component
            // such like showLoading and hideLoading
            chart: {
                type: Object,
                required: true,
                twoWay: true
            },
            // the chart's title
            // if it isn't necessary
            // it is fine to leave it.
            title: String,
            // options that you must apply in the component
            // check further information in the (docs)[http://echarts.baidu.com/index.html]
            option: {
                type: Object,
                required: true
            },
            width: {
                type: Number,
                default: 500
            },
            height: {
                type: Number,
                default: 300
            }
        },
        ready() {
            this.chart = Echarts.init(this.$els.chart);
            this.chart.setOption(this.option);
        },
        watch: {
            option(val) {
                console.log(val)
                this.chart.setOption(val);
            }
        }
    };
</script>

<style lang="css" scoped>
</style>
