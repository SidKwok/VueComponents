<template>
    <div id="app">
        <simple-table :options="options"
            ></simple-table>
        <button @click="dosth">do</button>
    </div>
</template>

<script>
    import Notification from './components/Notification/Notification';
    import SimpleTable from './components/SimpleTable/SimpleTable';

    export default {
        data() {
            return {
                show: false,
                options: {
                    titles: [{name: '日期'}, {name: '数量'}],
                    sortCols: [true, true],
                    data: [
                        ['20160105', 8],
                        ['20160203', 3],
                        ['20160808', 1],
                        ['20160301', 9],
                        ['20160703', 5],
                        ['20160105', 8],
                        ['20160203', 3],
                        ['20160808', 1],
                        ['20160301', 9],
                        ['20160703', 5],
                        ['20160105', 8],
                        ['20160203', 3],
                        ['20160808', 1],
                        ['20160301', 9],
                        ['20160703', 5],
                    ]
                }
            }
        },
        components: {
            Notification,
            SimpleTable
        },
        methods: {
            dosth() {
                this.show = !this.show;
            }
        }
    }
</script>

<style>

</style>
