<template>
    <div id="app">
        <!-- <tabs
            :titles="['pictures', 'articles', 'music']"
        >
            <p slot="pictures">pictures</p>
            <p slot="articles">articles</p>
            <p slot="music">music</p>
        </tabs> -->
        <div class="" v-for="i in 10" style="width: 100px;height: 100px;">
            <switch
                :checked.sync="checked"
                :height="20"
                :width="50"
            ></switch>
        </div>
        {{ checked }}
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

    export default {
        data() {
            return {
                show: false,
                checked: true
            }
        },
        components: {
            Toast,
            SimpleTable,
            DatePicker,
            Aside,
            Dialog,
            Switch,
        },
        methods: {
            dosth() {
                this.show = true
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
