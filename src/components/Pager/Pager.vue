<template lang="html">
    <ul class="pager">
        <li>&lt;</li><li :class="{active: page === i}" v-for="i in pageSize">{{ i + 1 }}</li><li>&gt;</li>
    </ul>
</template>

<script>
    export default {
        data() {
            return {
                page: 1
            }
        },
        props: {
            // all pages
            pageSize: {
                type: Number,
                required: true
            },
            // links show on pager
            maxLink: {
                type: Number,
                default: 6
            },
            // total items
            itemTotal: {
                type: Number,
                default: 0
            },
        }
    };
</script>

<style lang="css" scoped>
    .pager {

    }
    .pager li {
        display: inline-block;
        list-style: none;
        width: 25px;
        height: 25px;
        border: 1px #000 solid;
        border-left: none;
        text-align: center;
        line-height: 25px;
    }
    .pager li:nth-child(1) {
        border-left: 1px #000 solid;
    }
    .pager li .active {
        color: blue;
    }
</style>
