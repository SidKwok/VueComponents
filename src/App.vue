<template>
    <div id="app">
        <button @click="dosth">do</button>
        <dialog v-show="show"
            @close="show = false"
            title="yo"
            :show="show"
            ></dialog>
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
import Checkbox from './components/Checkbox/Checkbox';
import Dropdown from './components/Dropdown/Dropdown';
import Tags from './components/Tags/Tags';
import Calendar from './components/Calendar/Calendar';

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
            },
            list: [],
            options: [1, 2, 3],
            tags: [
                {
                    value: '你好吗你好吗啊啊啊',
                    text: '#8a89e0',
                    bg: '#e9e8f6'
                },
                {
                    value: 'GreatGreat',
                    text: '#30a1fe',
                    bg: '#e1effa'
                }
            ]
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
        Upload,
        Checkbox,
        Dropdown,
        Tags,
        Calendar
    },
    methods: {
        dosth(cur, pre) {
            this.show = !this.show
        },
        doConfirm() {
            console.log('yo im confirm')
        },
        doWarn() {
            console.log('yo warn me for what?? biatch!')
        }
    }
};
</script>

<style>
    body {
        height: 100%;
        width: 100%;
        margin: 0;
    }
    .test {
        width: 200px;
        overflow: hidden;
        text-overflow: ellipsis;
        border: 1px solid black;
        height: 100px;
    }
</style>
