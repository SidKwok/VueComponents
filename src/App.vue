<template>
    <div id="app">
        <h1>{{ date }}</h1>
        <button @click="dosth">do</button>
    </div>
</template>

<script>
    import Toast from './components/Toast/Toast';
    import SimpleTable from './components/SimpleTable/SimpleTable';
    import DatePicker from './components/DatePicker/DatePicker';

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
            DatePicker
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
