<template lang="html">
    <div class="tags">
        <template v-if="isDots">
            <span class="dot"
                v-for="dot in tags"
                :style="{
                    backgroundColor: dot.text
                    }"
            ></span>
        </template>
        <template v-else>
            <!-- <span v-for="tag in tags"
                :class="['wrapper', {'hint--bottom': true}]" :aria-label="tag.value">
                <span class="tag"
                    :style="{
                        border: `solid 1px ${tag.text}`,
                        color: tag.text,
                        backgroundColor: tag.bg
                        }"
                >{{ tag.value }}</span>
            </span> -->
            <span v-for="tag in tags"
                :class="['tag', {'hint--bottom': tag.text}]"
                :aria-label="tag.value"
                :style="{
                    border: `solid 1px ${tag.text}`,
                    color: tag.text,
                    backgroundColor: tag.bg
                    }"
            >{{ tag.value | ellipsis }}</span>
        </template>
    </div>
</template>

<script>
export default {
    props: {
        // {value: 'great', text: '#8a89e0', bg: '#e9e8f6'}
        // each tag should has the values above
        tags: {
            type: Array,
            required: true
        },
        // if the number of tags is more than this value
        // tags will turn to dots.
        limits: {
            type: Number,
            default: 9999
        }
    },
    computed: {
        isDots() {
            return this.tags.length > this.limits;
        }
    },
    filters: {
        ellipsis(val) {
            let bytesLength = val.replace(/[^\x00-\xff]/gi, "--").length;
            return bytesLength > 10
                ? val.slice(0, 4) + '...' : val;
        }
    }
};
</script>

<style lang="css" scoped>
    .tags {
        padding: 8px 2px;
        display: inline-block;
        width: 200px;
        border: 1px solid black;
        height: 200px;
    }
    .tag {
        height: 24px;
        padding: 1px 5px;
        /*box-sizing: border-box;*/
        margin: 2px 6px;
        display: inline-block;
        max-width: 100px;
        float: left;
        line-height: 25px;
    }
    .dot {
        width: 10px;
        height: 10px;
        border-radius: 100%;
        display: inline-block;
        margin: 0 5px;
    }

    [class*="hint--"] {
        position: relative;
        display: inline-block;
    }
    [class*="hint--"] {
        position: relative;
        display: inline-block;
    }
    [class*="hint--"]:before, [class*="hint--"]:after {
        position: absolute;
        -webkit-transform: translate3d(0, 0, 0);
        -moz-transform: translate3d(0, 0, 0);
        transform: translate3d(0, 0, 0);
        visibility: hidden;
        opacity: 0;
        z-index: 1000000;
        pointer-events: none;
        -webkit-transition: 0.3s ease;
        -moz-transition: 0.3s ease;
        transition: 0.3s ease;
        -webkit-transition-delay: 0ms;
        -moz-transition-delay: 0ms;
        transition-delay: 0ms;
    }
    [class*="hint--"]:hover:before, [class*="hint--"]:hover:after {
        visibility: visible;
        opacity: 1;
    }
    [class*="hint--"]:hover:before, [class*="hint--"]:hover:after {
        -webkit-transition-delay: 100ms;
        -moz-transition-delay: 100ms;
        transition-delay: 100ms;
    }
    [class*="hint--"]:before {
        content: '';
        position: absolute;
        background: transparent;
        border: 6px solid transparent;
        z-index: 1000001;
    }
    [class*="hint--"]:after {
        background: #383838;
        color: white;
        padding: 8px 10px;
        font-size: 12px;
        font-family: "Helvetica Neue", Helvetica, Arial, sans-serif;
        line-height: 12px;
        white-space: nowrap;
    }
    [class*="hint--"][aria-label]:after {
        content: attr(aria-label);
    }
    [class*="hint--"][data-hint]:after {
        content: attr(data-hint);
    }
    [aria-label='']:before,
    [aria-label='']:after,
    [data-hint='']:before,
    [data-hint='']:after {
        display: none !important;
    }
    .hint--bottom:before {
        border-bottom-color: #383838;
    }
    .hint--bottom:before {
        margin-top: -11px;
    }
    .hint--bottom:before, .hint--bottom:after {
        top: 100%;
        left: 50%;
    }
    .hint--bottom:before {
        left: calc(50% - 6px);
    }
    .hint--bottom:after {
        -webkit-transform: translateX(-50%);
        -moz-transform: translateX(-50%);
        transform: translateX(-50%);
    }
    .hint--bottom:hover:before {
        -webkit-transform: translateY(8px);
        -moz-transform: translateY(8px);
        transform: translateY(8px);
    }
    .hint--bottom:hover:after {
        -webkit-transform: translateX(-50%) translateY(8px);
        -moz-transform: translateX(-50%) translateY(8px);
        transform: translateX(-50%) translateY(8px);
    }
</style>
