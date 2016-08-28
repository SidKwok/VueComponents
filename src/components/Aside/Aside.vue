<template lang="html">
    <div class="aside" v-show="show">
        <div class="overlay" @click="close"></div>
        <div class="aside-content">
            <slot><slot>
        </div>
    </div>
</template>

<script>
    export default {
        props: {
            // has to be twoWay binding
            // it needs to be controled in an out
            show: {
                type: Boolean,
                default: false,
                twoWay: true
            },
            // aside content's title
            title: {
                type: String,
                default: '',
            }
        },
        methods: {
            close() {
                this.show = false;
            }
        },
        transitions: {
            slide: {
                enterClass: 'slideIn',
                leaveCLass: 'slideOut'
            },
            fade: {
                enterClass: 'fadeIn',
                leaveClass: 'fadeOut'
            }
        }
    };
</script>

<style lang="css" scoped>
    .aside {
        position: fixed;
        width: 100%;
        height: 100%;
    }
    .overlay {
        position: absolute;
        width: 100%;
        height: 100%;
        background-color: #000;
        opacity: .6;
        z-index: -1000;
        transition: all 1s;
    }
    .aside-content {
        width: 20%;
        height: 100%;
        background-color: #fff;
        z-index: -999;
    }
    /*.fadeIn {
        opacity: .6;
    }
    .fadeOut {
        opacity: 0;
    }*/
</style>
