<template>
    <div v-if="show" :transition="animation"
        :class="['toast', `n-${type}`]"
        :style="{
            width: `${width}px`,
            height: `${height}px`
            }"
        >
        <button class="close" @click="close"></button>
        <div class="content"
            :style="{
                width: `${width * 0.9}px`,
                height: `${height * 0.6}px`
                }">
            <slot></slot>
        </div>
    </div>
</template>

<script>
    export default {
        data() {
            return {
                timer: null
            }
        },
        props: {
            // show the toast or not,
            // has to be twoWay bind,
            // ensure that it can be control in and out
            show: {
                type: Boolean,
                default: false,
                twoWay: false
            },
            // toast type: normal, success, warn, fail
            type: {
                type: String,
                default: 'normal'
            },
            // animation type: bounceLeft, bounceRight
            animation: {
                type: String,
                default: 'bounceRight'
            },
            // expire time
            expire: {
                type: Number,
                default: 10000
            },
            width: {
                type: Number,
                default: 200
            },
            height: {
                type: Number,
                default: 100
            },
        },
        watch: {
            show(val) {
                if (val) {
                    this.timer = setTimeout(() => {
                        this.show = false;
                    }, this.expire);
                }
            }
        },
        methods: {
            close() {
                clearTimeout(this.timer);
                this.show = false;
            }
        },
        transitions: {
            bounceRight: {
                enterClass: 'bounceInRight',
                leaveClass: 'bounceOutRight'
            },
            bounceLeft: {
                enterClass: 'bounceInLeft',
                leaveClass: 'bounceOutLeft'
            }
        }
    }
</script>

<style scoped>
    .n-normal {
        background-color: #42afe3;
    }
    .n-success {
        background-color: #97cd76;
    }
    .n-warn {
        background-color: #fce473;
    }
    .n-fail {
        background-color: #ed6c63;
    }
    .toast {
        position: fixed;
        top: 10px;
        right: 10px;
        color: #fff;
        border-radius: 2px;
        font-size: 14px;
    }
    .toast .close{
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
    .toast .close::before {
        transform: rotate(45deg);
    }
    .toast .close::after {
        transform: rotate(-45deg);
    }
    .toast .close::before,
    .toast .close::after {
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
    .toast .content {
        margin: 35px auto 0 auto;
    }

    .bounceInRight {
        -webkit-animation:bounceInRight .6s .2s ease both;
        -moz-animation:bounceInRight .6s .2s ease both;
    }
    @-webkit-keyframes bounceInRight {
        0% {
            opacity:0;
            -webkit-transform:translateX(2000px)
        }
        60% {
            opacity:1;
            -webkit-transform:translateX(-30px)
        }
        80% {
            -webkit-transform:translateX(10px)
        }
        100% {
            -webkit-transform:translateX(0)
        }
    }
    @-moz-keyframes bounceInRight {
        0% {
            opacity:0;
            -moz-transform:translateX(2000px)
        }
        60% {
            opacity:1;
            -moz-transform:translateX(-30px)
        }
        80% {
            -moz-transform:translateX(10px)
        }
        100% {
            -moz-transform:translateX(0)
        }
    }

    .bounceOutRight {
        -webkit-animation:bounceOutRight .6s .2s ease both;
        -moz-animation:bounceOutRight .6s .2s ease both;
    }
    @-webkit-keyframes bounceOutRight {
        0% {
            -webkit-transform:translateX(0)}
        20% {
            opacity:1;
            -webkit-transform:translateX(-20px)
        }
        100% {
            opacity:0;
            -webkit-transform:translateX(2000px)}
        }
    @-moz-keyframes bounceOutRight {
        0% {
            -moz-transform:translateX(0)
        }
        20% {
            opacity:1;
            -moz-transform:translateX(-20px)
        }
        100% {
            opacity:0;
            -moz-transform:translateX(2000px)
        }
    }

    .bounceInLeft {
        -webkit-animation:bounceInLeft .6s .2s ease both;
        -moz-animation:bounceInLeft .6s .2s ease both;
    }
    @-webkit-keyframes bounceInLeft {
        0% {
            opacity:0;
            -webkit-transform:translateX(-2000px)
        }
        60% {
            opacity:1;
            -webkit-transform:translateX(30px)
        }
        80% {
            -webkit-transform:translateX(-10px)
        }
        100% {
            -webkit-transform:translateX(0)
        }
    }
    @-moz-keyframes bounceInLeft{
        0% {
            opacity:0;
            -moz-transform:translateX(-2000px)
        }
        60% {
            opacity:1;
            -moz-transform:translateX(30px)
        }
        80% {
            -moz-transform:translateX(-10px)
        }
        100% {
            -moz-transform:translateX(0)
        }
    }

    .bounceOutLeft {
        -webkit-animation:bounceOutLeft .6s .2s ease both;
        -moz-animation:bounceOutLeft .6s .2s ease both;
    }
    @-webkit-keyframes bounceOutLeft {
        0% {
            -webkit-transform:translateX(0)}
        20% {
            opacity:1;
            -webkit-transform:translateX(20px)
        }
        100% {
            opacity:0;
            -webkit-transform:translateX(-2000px)
        }
    }
    @-moz-keyframes bounceOutLeft {
        0% {
            -moz-transform:translateX(0)
        }
        20% {
            opacity:1;
            -moz-transform:translateX(20px)
        }
        100% {
            opacity:0;
            -moz-transform:translateX(-2000px)
        }
    }
</style>
