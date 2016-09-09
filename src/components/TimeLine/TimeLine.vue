<template lang="html">
    <div class="timeline">
        <template v-for="time in times">
            <div class="circle"></div>
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
    .circle {
        width: 20px;
        height: 20px;
        border-radius: 20px;
        border: 1px solid #000;
        margin: 2px auto;
        transition: transform 1s;
    }
    .circle:hover {
        transform: rotateY(360deg);
    }
    .circle:after {
        content: "";
        display: block;
        width: 10px;
        height: 10px;
        border-radius: 10px;
        margin: 5px auto;
        background-color: #000;
    }

    .line {
        height: 50px;
        width: 0px;
        border: 1px solid #000;
        margin: 0 auto;
    }
</style>
