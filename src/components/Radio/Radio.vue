<template lang="html">
    <label class="radio">
        <div class="radio-icon">
            <input type="radio" v-model="name" :value="value" :checked="checked">
            <div class="radio-circle" :style="[circleSize, circleStyle]">
                <div class="radio-dot" :style="[dotSize, dotStyle]"></div>
            </div>
        </div>
        <div class="radio-text">
            {{ value }}
        </div>
    </label>
</template>

<script>
export default {
    props: {
        // the radio group it belongs
        name: {
            type: String,
            required: true,
            twoWay: true
        },
        // it's value
        value: {
            type: String,
            required: true
        },
        // size of radio
        size: {
            type: Number,
            default: 16
        },
    },
    computed: {
        checked() {
            return this.name === this.value;
        },
        circleSize() {
            return {
                width: `${this.size}px`,
                height: `${this.size}px`
            };
        },
        circleStyle() {
            return {
                borderColor: this.checked ? '#2196f3' : 'rgba(0,0,0,.38)'
            };
        },
        dotSize() {
            return {
                width: `${this.size - 6}px`,
                height: `${this.size - 6}px`
            };
        },
        dotStyle() {
            return {
                opacity: this.checked ? 1 : 0
            };
        }
    }
};
</script>

<style lang="css" scoped>
    .radio {
        display: inline-block;
    }
    .radio .radio-icon input {
        display: none;
    }
    .radio-icon, .radio-text {
        display: inline-block;
        position: relative;
    }
    .radio-text {
        top: -5px;
    }
    .radio-circle {
        border-radius: 50%;
        border: 2px solid;
        background-color: transparent;
        transition: border-color .2s;
        position: relative;
    }
    .radio-dot {
        border-radius: 50%;
        background-color: #2196f3;
        transition: opacity .2s;
        position: absolute;
        top: 3px;
        left: 3px;
    }
</style>
