<template lang="html">
    <div class="aside" v-show="show" transition="fade">
        <div class="overlay" @click="close"></div>
        <div :style="{ width: `${width}px` }"
            :class="[
                'aside-content',
                {
                    'slideIn': show,
                    'slideOut': !show
                }
            ]">
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
            // set the width you want
            width: {
                type: Number,
                default: 350
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
                leaveClass: 'slideOut'
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
        top: 0px;
        left: 0px;
        width: 100%;
        height: 100%;
        transition: all .3s;
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
    .fadeIn {
        opacity: 1;
    }
    .fadeOut {
        opacity: 0;
    }
    .slideIn {
        animation:slideIn .3s;
    }
    .slideOut {
        animation:slideOut .3s;
    }
    @keyframes slideIn {
        0% {
            transform: translateX(-100%);
            opacity: 0;
        }
        100% {
            transform: translateX(0);
            opacity: 1;
        }
    }
    @keyframes slideOut {
        0% {
            transform: translateX(0);
            opacity: 1;
        }
        100% {
            transform: translateX(-100%);
            opacity: 0;
        }
    }
</style>
