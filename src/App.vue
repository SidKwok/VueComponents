<template>
    <div id="app">
        <button @click="dosth">do</button>
        <!-- <time-line :times="times"></time-line> -->
        <pager :page-size="pager.pageSize"></pager>
    </div>
</template>

<script>
    import Toast from 'components/Toast/Toast';
    import SimpleTable from './components/SimpleTable/SimpleTable';
    import DatePicker from './components/DatePicker/DatePicker';
    import Aside from './components/Aside/Aside';
    import Dialog from './components/Dialog/Dialog';
    import Tabs from './components/Tabs/Tabs';
    import Switch from './components/Switch/Switch';
    import Radio from './components/Radio/Radio';
    import FullPage from './components/FullPage/FullPage';
    import GoTop from './components/GoTop/GoTop';
    import Pager from './components/Pager/Pager';
    import TimeLine from './components/TimeLine/TimeLine';
    import Upload from './components/Upload/Upload';
    export default {
        data() {
            return {
                show: false,
                checked: true,
                picked: 'one',
                picked2: 'three',
                times: ['20:00', '21:00'],
                formData: null,
                pager: {
                    pageSize: 10
                }
            }
        },
        components: {
            Toast,
            SimpleTable,
            DatePicker,
            Aside,
            Dialog,
            Switch,
            Radio,
            FullPage,
            GoTop,
            Pager,
            TimeLine,
            Upload
        },
        methods: {
            dosth(err) {
                console.log(err)
            },
            doConfirm() {
                console.log('yo im confirm')
            },
            doWarn() {
                console.log('yo warn me for what?? biatch!')
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
