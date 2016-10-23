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
                twoWay: true
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
        margin: 20px auto 0 auto;
    }

    /*Animations*/
    .bounceRight-transition,
    .bounceLeft-transition {
        animation-duration: .6s;
        animation-fill-mode: both;
    }
    .bounceRight-enter {
        animation-name: bounceInRight;
    }
    @keyframes bounceInRight {
        from, 60%, 75%, 90%, to {
            animation-timing-function: cubic-bezier(0.215, 0.610, 0.355, 1.000);
        }

        from {
            opacity: 0;
            transform: translate3d(3000px, 0, 0);
        }

        60% {
            opacity: 1;
            transform: translate3d(-25px, 0, 0);
        }

        75% {
            transform: translate3d(10px, 0, 0);
        }

        90% {
            transform: translate3d(-5px, 0, 0);
        }

        to {
            transform: none;
        }
    }
    .bounceRight-leave {
        animation-name: bounceOutRight;
    }
    @keyframes bounceOutRight {
        20% {
            opacity: 1;
            transform: translate3d(-20px, 0, 0);
        }

        to {
            opacity: 0;
            transform: translate3d(2000px, 0, 0);
        }
    }

    .bounceLeft-enter {
        animation-name: bounceInLeft;
    }
    @keyframes bounceInLeft {
        from, 60%, 75%, 90%, to {
            animation-timing-function: cubic-bezier(0.215, 0.610, 0.355, 1.000);
        }

        0% {
            opacity: 0;
            transform: translate3d(-3000px, 0, 0);
        }

        60% {
            opacity: 1;
            transform: translate3d(25px, 0, 0);
        }

        75% {
            transform: translate3d(-10px, 0, 0);
        }

        90% {
            transform: translate3d(5px, 0, 0);
        }

        to {
            transform: none;
        }
    }
    .bounceLeft-leave {
        animation-name: bounceOutLeft;
    }
    @keyframes bounceOutLeft {
        20% {
            opacity: 1;
            transform: translate3d(20px, 0, 0);
        }

        to {
            opacity: 0;
            transform: translate3d(-2000px, 0, 0);
        }
    }
</style>
