<template>
    <div id="app">
        <dialog :show.sync="show"
            title="yoyoyo"
            type="success"
            @confirm="doConfirm"
            @warn="doWarn"
        >
            <h1>hey you</h1>
            <p>
                Jesse Pinkmen is in the house!
            </p>
        </dialog>
        <!-- <aside :show.sync="show"></aside> -->
        <button @click="dosth">do</button>
    </div>
</template>

<script>
    import Toast from './components/Toast/Toast';
    import SimpleTable from './components/SimpleTable/SimpleTable';
    import DatePicker from './components/DatePicker/DatePicker';
    import Aside from './components/Aside/Aside';
    import Dialog from './components/Dialog/Dialog';

    export default {
        data() {
            return {
                show: false,
                date: '',
            }
        },
        components: {
            Toast,
            SimpleTable,
            DatePicker,
            Aside,
            Dialog
        },
        methods: {
            dosth() {
                this.show = !this.show;
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
