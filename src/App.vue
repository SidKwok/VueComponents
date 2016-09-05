<template>
    <div id="app">
        <!-- <br />
        <div style="text-align: center;">
            <radio :name.sync="picked" value="one"></radio>
            <radio :name.sync="picked" value="two"></radio>

            <radio :name.sync="picked2" value="three" :size="20"></radio>
            <radio :name.sync="picked2" value="four" :size="20"></radio>
        </div>
        <button @click="dosth">do</button> -->
        <!-- <div v-fullpage>
            <div></div>
            <div></div>
            <div></div>
            <div></div>
        </div> -->
        <full-page :pages="3" @enter="dosth">
            <template slot="page-1">1</template>
            <template slot="page-2">2</template>
            <template slot="page-3">3</template>
        </full-page>
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

    import fullpage from './directives/fullpage/fullpage';

    export default {
        data() {
            return {
                show: false,
                checked: true,
                formdata: {},
                picked: 'one',
                picked2: 'three'
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
            FullPage
        },
        directives: {
            fullpage
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
