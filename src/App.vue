<template>
    <div id="app">
        <notification
            :show.sync="show"
            animation="bounceLeft"
            type="success"
            :expire="1000"
        >
            Vue is gas!
        </notification>
        <button @click="dosth">do</button>
    </div>
</template>

<script>
    import Notification from './components/Notification/Notification';

    export default {
        data() {
            return {
                show: false
            }
        },
        components: {
            Notification
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
