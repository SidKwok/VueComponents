<template>
    <div id="app">
        <br />
        <div style="text-align: center;">
            <upload-image
                :formdata.sync="formdata"
                @error="dosth"
            ></upload-image>
        </div>
        <button @click="dosth">do</button>
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

    export default {
        data() {
            return {
                show: false,
                checked: true,
                formdata: {}
            }
        },
        components: {
            Toast,
            SimpleTable,
            DatePicker,
            Aside,
            Dialog,
            Switch,
            UploadImage
        },
        methods: {
            dosth() {
                console.log('yoyo');
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
