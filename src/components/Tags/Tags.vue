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
            <span class="tag"
                v-for="tag in tags"
                :style="{
                    border: `solid 1px ${tag.text}`,
                    color: tag.text,
                    backgroundColor: tag.bg
                    }"
            >{{ tag.value }}</span>
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
    }
};
</script>

<style lang="css" scoped>
    .tags {
        padding: 8px 2px;
        display: inline-block;
    }
    .tag {
        height: 20px;
        padding: 3px 5px;
        box-sizing: border-box;
        margin: 0 5px;
        text-align: center;
        /*display: inline-block;*/
        max-width: 100px;
        overflow: hidden;
    }
    .dot {
        width: 10px;
        height: 10px;
        border-radius: 100%;
        display: inline-block;
        margin: 0 5px;
    }
</style>
