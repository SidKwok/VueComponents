<template lang="html">
    <div class="dialog" transition="zoom">
        <div class="overlay" @click="$emit('close')"></div>
        <div class="dialog-box"
            :style="{width: width + 'px'}">
            <div class="dialog-header">
                <p class="title">{{ title }}</p>
                <a href="javascript: void(0);" class="close" @click="$emit('close')"></a>
            </div>
            <div class="dialog-content">
                <div :class="['icon', type + '-icon']" v-if="type !== 'normal'"></div>
                <slot></slot>
            </div>
            <div class="dialog-footer">
                <div :class="['btns-group', btnPos === 'right' ? 'right' : '']">
                    <a href="javascript: void(0);" v-show="type === 'normal' && showNormal"
                        class="dialog-btn normal-btn" @click="$emit('normal')">{{ normalText }}</a>
                    <a href="javascript: void(0);" v-show="type === 'confirm'"
                        class="dialog-btn confirm-btn" @click="$emit('confirm')"
                        >{{ confirmText }}</a>
                        <a href="javascript: void(0);" v-show="type === 'warn'"
                            class="dialog-btn warn-btn">{{ warnText }}</a>
                    <a href="javascript: void(0);"
                        class="dialog-btn cancel-btn"
                        @click="$emit('close')">{{ cancelText }}</a>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
export default {
    props: {
        type: {
            type: String,
            default: 'normal' // success, fail, warn, confirm
        },
        title: String,
        normalText: {
            type: String,
            default: '保存'
        },
        warnText: {
            type: String,
            default: '确认'
        },
        confirmText: {
            type: String,
            default: '确认'
        },
        cancelText: {
            type: String,
            default: '取消'
        },
        btnPos: {
            type: String,
            default: 'middle'
        },
        width: {
            type: Number,
            default: 400
        },
        showNormal: {
            type: Boolean,
            default: true
        }
    }
};
</script>

<style lang="less" scoped>
    .dialog {
        position: fixed;
        width: 100%;
        height: 100%;
        top: 0px;
        left: 0px;
        z-index: 9999;

        .overlay {
            position: absolute;
            width: 100%;
            height: 100%;
            background-color: #000;
            opacity: .5;
            z-index: -1000;
        }

        .dialog-box {
            position: relative;
            top: 25%;
            min-height: 200px;
            border: 1px solid #ddd;
            background-color: #fff;
            border-radius: 4px;
            margin: 0 auto;

            .dialog-header {
                position: absolute;
                top: 0;
                left: 0;
                height: 48px;
                width: 100%;

                .title {
                    font-size: 18px;
                    position: absolute;
                    top: 12px;
                    left: 24px;
                }

                .close{
                    background-color: #fff;
                    border: none;
                    border-radius: 0 3px;
                    cursor: pointer;
                    display: inline-block;
                    height: 24px;
                    position: absolute;
                    vertical-align: top;
                    width: 24px;
                    top: 16px;
                    right: 24px;

                    &::before {
                        transform: rotate(45deg);
                    }
                    &::after {
                        transform: rotate(-45deg);
                    }
                    &::before,
                    &::after {
                        background-color: #888;
                        content: "";
                        display: block;
                        height: 1px;
                        left: 50%;
                        margin-left: -25%;
                        margin-top: -1px;
                        position: absolute;
                        top: 50%;
                        width: 50%;
                    }
                }
            }

            .dialog-content {
                padding: 48px 24px 80px 24px;
                height: 100%;

                .icon {
                    width: 60px;
                    height: 60px;
                    margin: 0 auto 16px auto;
                }
                .success-icon {
                    background-image: url('../assets/images/icon/dialog-success.svg');
                }
                .fail-icon {
                    background-image: url('../assets/images/icon/dialog-fail.svg');
                }
                .warn-icon {
                    background-image: url('../assets/images/icon/dialog-warn.svg');
                }
                .confirm-icon {
                    background-image: url('../assets/images/icon/dialog-confirm.svg');
                }
            }

            .dialog-footer {
                position: absolute;
                width: 100%;
                height: 80px;
                bottom: 0;
                left: 0;

                .btns-group {
                    display: block;
                    margin: 16px auto 0 auto;
                    width: 285px;

                    .dialog-btn {
                        display: inline-block;
                        width: 88px;
                        height: 32px;
                        margin: 0 10px;
                        line-height: 32px;
                        text-align: center;
                        font-size: 14px;
                    }
                    .normal-btn {
                        background-color: #008cff;
                        border: 1px solid #008cff;
                        border-radius: 2px;
                        color: #fff;
                    }
                    .confirm-btn {
                        background-color: #ff3b30;
                        border: 1px solid #ff3b30;
                        border-radius: 2px;
                        color: #fff;
                    }
                    .warn-btn {
                        background-color: #ff9500;
                        border: 1px solid #ff9500;
                        border-radius: 2px;
                        color: #fff;
                    }
                    .cancel-btn {
                        background-color: #fff;
                        border: 1px solid #ddd;
                        border-radius: 2px;
                        color: #333;
                    }
                }
                .right {
                    width: auto;
                    text-align: right;
                    // margin: auto 12px;
                    margin-right: 12px;
                }
            }
        }
    }
    /*Animations*/
    .zoom-transition,
    .zoom-transition .dialog-box {
        transition: .3s;
    }
    .zoom-enter,
    .zoom-leave {
        opacity: 0;
    }
    .zoom-enter .dialog-box,
    .zoom-leave .dialog-box {
        transform: scale(.5);
    }
</style>
