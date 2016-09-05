<template lang="html">
    <div v-el:fullpage
        class="fullpage"
        @mousewheel="switchPage"
    >
        <div class="container"
            :style="{height: `${pageHeight * pages}px`, top: conPos}"
        >
            <div class="page" v-for="i of pages" :style="{top: `${i * pageHeight}px`}">
                <slot :name="`page-${i + 1}`"></slot>
            </div>
        </div>
        <div class="nav"
            :style="{top: navPos}"
            @click="switchPage"
            v-el:nav
        >
            <ul>
                <li v-for="i of pages"
                    :data-page="i + 1"
                >
                    <a href="#"
                        :data-page="i + 1"
                        class="dot"
                        :style="{backgroundColor: (i + 1) === currentPage ? '#000' : ''}"
                    ></a>
                </li>
            </ul>
        </div>
    </div>
</template>

<script>
    export default {
        data() {
            return {
                currentPage: 1,
                pageHeight: 0,
                scrolling: false
            }
        },
        props: {
            // how many pages you want to show
            pages: {
                type: Number,
                required: true
            },
        },
        computed: {
            conPos() {
                return `-${(this.currentPage - 1) * this.pageHeight}px`;
            },
            navPos() {
                return `${this.pageHeight / 2 - this.$els.nav.clientHeight / 2}px`
            }
        },
        ready() {
            let fullpage = this.$els.fullpage;
            this.pageHeight = fullpage.clientHeight;
            window.onresize = () => {
                this.pageHeight = fullpage.clientHeight;
            };
        },
        methods: {
            switchPage(event) {
                if (!this.scrolling) {
                    this.scrolling = true;
                    if (event.target.dataset.page) {
                        this.currentPage = parseInt(event.target.dataset.page);
                    } else {
                        let index = (event.wheelDelta < 0) ? 1 : -1;
                        this.currentPage = (this.currentPage + index) > this.pages
                                            ? this.currentPage
                                            : this.currentPage + index
                    }
                    setTimeout(() => {
                        this.scrolling = false;
                    }, 1000);
                }
            },
        },
    };
</script>

<style lang="css" scoped>
    .fullpage {
        position: fixed;
        top: 0px;
        left: 0px;
        height: 100%;
        width: 100%;
    }
    .container {
        position: relative;
        width: 100%;
        transition: top 1s;
    }
    .page {
        position: absolute;
        width: 100%;
        height: 100%;
    }
    .nav {
        position: fixed;
        right: 10px;
    }
    .nav ul {
        padding: 0;
        margin: 0;
    }
    .nav li {
        list-style-type: none;
        width: 15px;
        height: 15px;
        padding-top: 10px;
    }
    .nav .dot {
        display: inline-block;
        height: 12px;
        width: 12px;
        border-radius: 12px;
        border: 1px solid;
    }
</style>
