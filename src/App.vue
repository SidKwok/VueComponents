<template>
    <div id="app">
        <!-- <pages :counts="4"></pages> -->
        <button @click="dosth">do</button>
        <time-line :times="times"></time-line>
    </div>
</template>

<script>
    import Toast from './components/Toast/Toast';
    import SimpleTable from './components/SimpleTable/SimpleTable';
    import DatePicker from './components/DatePicker/DatePicker';
    import Aside from './components/Aside/Aside';
    import Dialog from './components/Dialog/Dialog';
    import Tabs from './components/Tabs/Tabs';
    import Switch from './components/Switch/Switch';
    import UploadImage from './components/UploadImage/UploadImage';
    import Radio from './components/Radio/Radio';
    import FullPage from './components/FullPage/FullPage';
    import GoTop from './components/GoTop/GoTop';
    import Pages from './components/Pages/Pages';
    import TimeLine from './components/TimeLine/TimeLine';
    export default {
        data() {
            return {
                show: false,
                checked: true,
                formdata: {},
                picked: 'one',
                picked2: 'three',
                times: ['20:00', '21:00']
            }
        },
        components: {
            Toast,
            SimpleTable,
            DatePicker,
            Aside,
            Dialog,
            Switch,
            UploadImage,
            Radio,
            FullPage,
            GoTop,
            Pages,
            TimeLine
        },
        methods: {
            dosth(cp, pp) {
                console.log(cp, pp)
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
