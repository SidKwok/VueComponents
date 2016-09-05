<template lang="html">
    <div v-el:fullpage
        class="fullpage"
    >
        <div class="container"
            :style="{height: `${pageHeight * pages}px`, top: conPos}"
        >
            <div class="page" v-for="i of pages" :style="{top: `${i * pageHeight}px`}">
                <slot :name="`page-${i + 1}`"></slot>
            </div>
        </div>
        <div class="nav">
            <button @click="switchPage(1)">1</button>
            <button @click="switchPage(2)">2</button>
            <button @click="switchPage(3)">3</button>
        </div>
    </div>
</template>

<script>
    export default {
        data() {
            return {
                currentPage: 1,
                pageHeight: 0
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
            }
        },
        ready() {
            this.pageHeight = this.$els.fullpage.clientHeight;
            window.onresize = () => {
                this.pageHeight = this.$els.fullpage.clientHeight;
            };
        },
        methods: {
            switchPage(index) {
                this.currentPage = index;
            }
        }
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
        border: 1px solid;
        position: absolute;
        width: 100%;
        height: 100%;
    }
    .nav {
        position: fixed;
        top: 10px;
        right: 10px;
    }
</style>
