<template lang="html">
    <label class="switch" :class="{ disabled: disabled }">
        <div class="switch-bar"
            :style="[
                barSize,
                barColor
            ]"
        >
            <div class="switch-circle"
                :style="[
                    circleSize,
                    circleColor,
                    circlePos
                ]"
            ></div>
        </div>
        <div class="switch-tag" v-if="!hideTag">
            <slot></slot>
        </div>
        <input type="checkbox" v-model="checked">
    </label>
</template>

<script>
    export default {
        props: {
            // need twoWay binding to
            // send the value outside
            checked: {
                type: Boolean,
                default: false,
                twoWay: true
            },
            // show Tagname or not
            hidetag: {
                type: Boolean,
                default: true,
            },
            // disabled switch
            disabled: {
                type: Boolean,
                default: false
            },
            // they belong to the bar
            width: {
                type: Number,
                default: 34,
            },
            height: {
                type: Number,
                default: 14
            }
        },
        computed: {
            barSize() {
                return {
                    width: `${this.width}px`,
                    height: `${this.height}px`
                };
            },
            barColor() {
                let style = {};
                if (this.disabled) {
                    style.backgroundColor = 'rgba(0,0,0,.12)';
                } else {
                    this.checked
                        ? style.backgroundColor = 'rgba(33,150,243,.5)'
                        : style.backgroundColor = 'rgba(0,0,0,.26)';
                }
                return style;
            },
            circleSize() {
                let width = this.height + 6;
                let height = width;

                return {
                    width: `${width}px`,
                    height: `${height}px`,
                };
            },
            circlePos() {
                let left = this.checked
                    ? `${this.width - this.height - 6}px`
                    : '0px';
                return {
                    left: left
                }
            },
            circleColor() {
                let style = {};
                if (this.disabled) {
                    style.backgroundColor = '#bdbdbd';
                } else {
                    style.backgroundColor
                        = this.checked ? '#2196f3' : '#fafafa'
                }
                return style;
            }
        }
    };
</script>

<style lang="css" scoped>
    .switch {
        display: inline-block;
    }
    .disabled {
        pointer-events: none;
    }
    .disabled:hover {
        cursor: not-allowed;
    }
    .switch-bar {
        position: relative;
        display: inline-block;
        border-radius: 8px;
        cursor: pointer;
        transition: all .2s;
    }
    .switch-circle {
        position: absolute;
        display: inline-block;
        box-shadow: 0 1px 3px rgba(0,0,0,.4);
        border-radius: 50%;
        top: -3px;
        transition: all .2s;
    }
    .switch-tag {
        display: inline-block;
    }
    .switch input {
        display: none;
    }
</style>
