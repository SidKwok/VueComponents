<template lang="html">
    <ul class="pager" @click="switchPage($event)">
        <li :data-page="currentPage - 1">&lt;</li><li :data-page="i + 1" :class="{active: currentPage === (i + 1)}" v-for="i in pageSize">{{ i + 1 }}</li><li :data-page="currentPage + 1">&gt;</li>
    </ul>
</template>

<script>
    export default {
        data() {
            return {
                currentPage: 1
            }
        },
        props: {
            // all pages
            pageSize: {
                type: Number,
                required: true
            },
            // links show on pager
            maxLinks: {
                type: Number,
                default: 6
            },
            // total items
            itemTotal: {
                type: Number,
                default: 0
            },
        },
        methods: {
            switchPage(e) {
                let page = parseInt(e.target.dataset.page);
                if (page <= this.pageSize && page > 0) {
                    this.$emit('switchpage', page, this.currentPage);
                    this.currentPage = page;
                }
            }
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
    .active {
        color: blue;
    }
</style>
