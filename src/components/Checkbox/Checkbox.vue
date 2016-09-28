<template lang="html">
    <label class="checkbox">
        <div :class="['checkmark', {'active': isChecked}]"></div>
        <span class="text"><slot>{{ value }}</slot></span>
        <input type="checkbox" :value="value" v-model="group" style="display: none;">
    </label>
</template>

<script>
    export default {
        props: {
            // value of the checkbox
            value: {
                type: String,
                required: true
            },
            // the group it is belonged to
            // has to be two way binding
            group: {
                required: true,
                twoWay: true
            },
            // show the text if exists
            text: {
                type: String,
                default: ''
            }
        },
        computed: {
            isChecked() {
                return this.group.includes(this.value);
            }
        }
    };
</script>

<style lang="css" scoped>
    .checkbox {
        display: inline-block;
        width: auto;
    }
    .checkmark {
        display: inline-block;
        width: 20px;
        height: 20px;
        position: relative;
        border-radius: 2px;
        border: 2px solid rgba(0,0,0,.38);
        transition: all .3s ease;
    }
    .checkmark:after {
        box-sizing: border-box;
        position: absolute;
        display: block;
        content: "";
    }
    .active {
        background: #2196f3;
        border-color: #2196f3;
    }
    .active:after {
        left: 7px;
        bottom: 5px;
        width: 6px;
        height: 13px;
        transform: rotate(45deg);
        border-right: 2px solid #fff;
        border-bottom: 2px solid #fff;
    }
    .text {
        display: inline-block;
        font-size: 16px;
        position: relative;
        top: -6px;
        margin-left: 8px;
    }
</style>
