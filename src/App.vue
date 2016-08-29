<template>
    <div id="app">
        <!-- <tabs
            :titles="['pictures', 'articles', 'music']"
        >
            <p slot="pictures">pictures</p>
            <p slot="articles">articles</p>
            <p slot="music">music</p>
        </tabs> -->
        <dialog :show.sync="show"
            title="yoyoyo"
            type="success"
            :width="500"
            :height="300"
            @confirm="doConfirm"
            @warn="doWarn"
        >
            <h1>hey you</h1>
            <p>
                Jesse Pinkmen is in the house!
            </p>
        </dialog>
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
