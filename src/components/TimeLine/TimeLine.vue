<template lang="html">
    <div class="timeline">
        <template v-for="time in times">
            <div class="dot"></div>
            <div class="line"></div>
        </template>
    </div>
</template>

<script>
    export default {
        props: {
            // length of the line
            length: {
                type: Number,
                default: 500
            },
            // every specific time is a dot
            times: {
                type: Array,
                required: true
            }
        }
    };
</script>

<style lang="css" scoped>
    .timeline {
        width: 100px;
    }
    .dot {
        width: 25px;
        height: 25px;
        border-radius: 25px;
        background-color: #000;
        margin: 2px auto;
    }
    .line {
        height: 50px;
        width: 0px;
        border: 2px solid #000;
        margin: 0 auto;
    }
</style>
