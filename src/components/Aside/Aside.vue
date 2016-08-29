<template lang="html">
    <div class="aside" v-show="show" transition="fade">
        <div class="overlay" @click="close"></div>
        <div v-show="show"
            :style="contentStyle"
            class="aside-content"
            :transition="`slide-${position}`"
        >
            <div class="aside-title">
                <h4>{{ title }}</h4>
                <button class="close" @click="close"></button>
            </div>
            <div class="aside-body">
                <slot><slot>
            </div>
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
            },
            // position of aside: left, right
            position: {
                type: String,
                default: 'left'
            },
            // set the width you want
            width: {
                type: Number,
                default: 350
            }
        },
        computed: {
            contentStyle() {
                let style = {
                    width: `${this.width}px`
                };
                this.position === 'left'
                    ? style.left = 0
                    : style.right = 0;
                return style;
            }
        },
        methods: {
            close() {
                this.show = false;
            }
        },
    };
</script>

<style lang="css" scoped>
    .aside {
        position: fixed;
        top: 0px;
        left: 0px;
        width: 100%;
        height: 100%;
    }
    .overlay {
        position: absolute;
        width: 100%;
        height: 100%;
        background-color: #000;
        opacity: .5;
        z-index: -1000;
    }
    .aside-content {
        position: absolute;
        height: 100%;
        background-color: #fff;
        overflow: auto;
        z-index: -999;
    }
    .aside-title {
        position: relative;
        border-bottom: 1px solid #e5e5e5;
        min-height: 16.43px;
        padding: 6px 15px;
        background: #337ab7;
        color: #fff
    }
    .aside-title .close{
        background-color: rgba(17, 17, 17, 0.2);
        border: none;
        border-radius: 0 3px;
        cursor: pointer;
        display: inline-block;
        height: 24px;
        position: absolute;
        vertical-align: top;
        width: 24px;
        top: 0px;
        right: 0px;
    }
    .aside-title .close::before {
        transform: rotate(45deg);
    }
    .aside-title .close::after {
        transform: rotate(-45deg);
    }
    .aside-title .close::before,
    .aside-title .close::after {
        background-color: #fff;
        content: "";
        display: block;
        height: 2px;
        left: 50%;
        margin-left: -25%;
        margin-top: -1px;
        position: absolute;
        top: 50%;
        width: 50%;
    }
    .aside-body {
        position: relative;
        padding: 15px;
    }
    /*Animations*/
    .fade-transition {
        transition: all .3s;
    }
    .fade-enter, .fade-leave {
        opacity: 0;
    }
    .slide-left-transition,
    .slide-right-transition {
        animation-duration: .3s;
        animation-fill-mode: both;
    }

    .slide-left-enter {
        animation-name: slideLeftIn;
    }
    .slide-left-leave {
        animation-name: slideLeftOut;
    }
    @keyframes slideLeftIn {
        0% {
            transform: translateX(-100%);
            opacity: 0;
        }
        100% {
            transform: translateX(0);
            opacity: 1;
        }
    }
    @keyframes slideLeftOut {
        0% {
            transform: translateX(0);
            opacity: 1;
        }
        100% {
            transform: translateX(-100%);
            opacity: 0;
        }
    }

    .slide-right-enter {
        animation-name: slideRightIn;
    }
    .slide-right-leave {
        animation-name: slideRightOut;
    }
    @keyframes slideRightIn {
        0% {
            transform: translateX(200%);
            opacity: 0;
        }
        100% {
            transform: translateX(0);
            opacity: 1;
        }
    }
    @keyframes slideRightOut {
        0% {
            transform: translateX(0);
            opacity: 1;
        }
        100% {
            transform: translateX(200%);
            opacity: 0;
        }
    }
</style>
