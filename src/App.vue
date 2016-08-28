<template>
    <div id="app">
        <simple-table
            :data="data"
            :titles="titles"
            :sortcols="sortcols"
            :pagecount="5"
        ></simple-table>
        <button @click="dosth">do</button>
    </div>
</template>

<script>
    import Toast from './components/Toast/Toast';
    import SimpleTable from './components/SimpleTable/SimpleTable';
    import DatePicker from './components/DatePicker/DatePicker';
    import Aside from './components/Aside/Aside';

    export default {
        data() {
            return {
                show: false,
                date: '',
                // titles name
                titles: [{name: 'date'}, {name: 'number'}],
                // the cols you need to sort
                sortcols: [true, true],
                // please ensure that that length of each row
                // is the same as titles' length
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
                ]
            }
        },
        components: {
            Toast,
            SimpleTable,
            DatePicker,
            Aside
        },
        methods: {
            dosth() {
                this.show = !this.show;
            }
        }
    }
</script>

<style>
    body {
        height: 100%;
        width: 100%;
        margin: 0;
    }
</style>
