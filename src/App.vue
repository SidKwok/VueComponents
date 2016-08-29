<template>
    <div id="app">
        <!-- <tabs
            :titles="['pictures', 'articles', 'music']"
        >
            <p slot="pictures">pictures</p>
            <p slot="articles">articles</p>
            <p slot="music">music</p>
        </tabs> -->
        <aside
            :show.sync="show"
            title="yo im aside"
            :width="300"
            position="left"
        >
            <h1>yoyo</h1>
            <p v-for="i in 10">what's up biatch!</p>
        </aside>
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

    export default {
        data() {
            return {
                show: false,
            }
        },
        components: {
            Toast,
            SimpleTable,
            DatePicker,
            Aside,
            Dialog,
            Tabs,
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
