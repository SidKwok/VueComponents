<template>
    <div id="app">
        <aside
            :show.sync="show"
        ></aside>
        <date-picker
            :date.sync="date"
            lang="zh"></date-picker>
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
                date: ''
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
