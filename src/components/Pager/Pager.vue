<template lang="html">
    <div class="pager">
        <ul class="pager-nav" @click="switchPage($event)">
            <li :data-page="(currentPage - 1 === 0) ? currentPage : currentPage - 1"
            ><i class="fa fa-angle-left"></i></li>
            <li :class="{ active: currentPage === 1 }"
                data-page="1"
              v-if="pageCount > 0">1</li>
            <li v-if="showPrevMore">...</li>
            <li v-for="item in pagers"
                :class="{active: currentPage === item}"
                :data-page="item"
            >{{ item }}</li>
            <li v-if="showNextMore">...</li>
            <li :class="{ active: currentPage === pageCount }"
                :data-page="pageCount"
              v-if="pageCount > 1">{{ pageCount }}</li>
            <li :data-page="(currentPage + 1 > pageCount) ? pageCount : currentPage + 1"
            ><i class="fa fa-angle-right"></i></li>
        </ul>
        <a class="pager-size" href="javascript: void(0);" v-el:pager-size>
            <span class="pager-size-select">
                {{ pageSize }} 条/页 <i class="fa fa-caret-down"></i>
            </span>
            <ul class="pager-size-options" @click="switchPageSize($event)">
                <li data-page-size="5">5 条/页</li>
                <li data-page-size="10">10 条/页</li>
                <li data-page-size="20">20 条/页</li>
            </ul>
        </a>
        <span class="pager-count">共 {{ count }} 条</span>
    </div>
</template>

<script>
export default {
    data() {
        return {
            pageSize: 10,
            currentPage: 1,
            showPrevMore: false,
            showNextMore: false
        };
    },
    props: {
        count: Number,
        pagerCount: {
            type: Number,
            default: 7
        }
    },
    computed: {
        pageCount() {
            return Math.trunc(this.count / this.pageSize + 1);
        },
        pagers() {
            const pagerCount = this.pagerCount;

            const currentPage = Number(this.currentPage);
            const pageCount = Number(this.pageCount);

            let showPrevMore = false;
            let showNextMore = false;

            if (pageCount > pagerCount) {
                if (currentPage > pagerCount - 2) {
                    showPrevMore = true;
                }

                if (currentPage < pageCount - 2) {
                    showNextMore = true;
                }
            }

            const array = [];

            if (showPrevMore && !showNextMore) {
                const startPage = pageCount - (pagerCount - 2);
                for (let i = startPage; i < pageCount; i++) {
                    array.push(i);
                }
            } else if (!showPrevMore && showNextMore) {
                for (let i = 2; i < pagerCount; i++) {
                    array.push(i);
                }
            } else if (showPrevMore && showNextMore) {
                const offset = Math.floor(pagerCount / 2) - 1;
                for (let i = currentPage - offset; i <= currentPage + offset; i++) {
                    array.push(i);
                }
            } else {
                for (let i = 2; i < pageCount; i++) {
                    array.push(i);
                }
            }

            this.showPrevMore = showPrevMore;
            this.showNextMore = showNextMore;

            return array;
        }
    },
    methods: {
        switchPageSize(e) {
            const pageSize = e.target.dataset.pageSize;
            this.pageSize = Number(pageSize) || this.pageSize;
            // 初始化pager
            this.currentPage = 1;
            // 让选择器失去焦点
            this.$els.pagerSize.blur();
            this.$emit('update', {
                page: this.currentPage + '',
                limit: this.pageSize + ''
            });
        },
        switchPage(e) {
            if (e.target.dataset.page) {
                let currentPage = Number(e.target.dataset.page);
                if (currentPage !== this.currentPage) {
                    this.currentPage = Number(e.target.dataset.page);
                    this.$emit('update', {
                        page: this.currentPage + '',
                        limit: this.pageSize + ''
                    });
                }
            }
        }
    },
    events: {
        initPager() {
            this.currentPage = 1;
            this.pageSize = 10;
            this.showPrevMore = false;
            this.showNextMore = false;
        }
    }
};
</script>

<style lang="less" scoped>
    .pager {
        font-size: 14px;
        height: 120px;
        margin: 16px 0px;
        &-count {
            display: inline-block;
            float: right;
            width: 88px;
            height: 32px;
            text-align: center;
            line-height: 32px;
            margin-left: 16px;
        }

        &-size {
            display: inline-block;
            float: right;
            width: 112px;
            height: 32px;
            border: solid 1px #ddd;
            border-radius: 2px;
            text-align: center;
            line-height: 32px;
            margin-left: 16px;
            cursor: pointer;

            &-select {
                color: #333;
                i {
                    color: #ddd;
                    margin-left: 4px;
                    transition: .3s;
                }
            }

            &:focus > &-options {
                display: block;
            }
            &:focus > &-select i {
                transform: rotate(180deg);
            }

            &-options {
                position: absolute;
                width: 112px;
                box-shadow: 0px 0px 10px 0px rgba(0, 0, 0, 0.2);
                background-color: #fff;
                z-index: 100;
                border-radius: 2px;
                display: none;
                padding: 8px 0px;

                li {
                    height: 32px;
                    // padding-left: 16px;
                    line-height: 32px;
                    cursor: pointer;

                    &:hover {
                        background-color: #ebf5fd;
                    }
                }
            }
        }

        &-nav {
            display: inline-block;
            float: right;
            height: 33px;
            line-height: 32px;
            border: solid 1px #ddd;
            border-radius: 2px;
            margin-left: 16px;

            li {
                float: left;
                min-width: 32px;
                text-align: center;
                border-left: solid 1px #ddd;
                // transition: .1s;
                cursor: pointer;
            }
            li:nth-child(1) {
                border-left: none;
            }
            li:hover,
            .active {
                border-color: #008cff;
                background-color: #008cff;
                color: #fff;
            }
        }
    }
</style>
