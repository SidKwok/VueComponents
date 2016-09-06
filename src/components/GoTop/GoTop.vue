<template lang="html">
    <div :style="{bottom: `${bottom}px`, right: `${right}px`}"
        class="goTop"
        @click="scroll"
    >

    </div>
</template>

<script>
    export default {
        props: {
            bottom: {
                type: Number,
                default: 10
            },
            right: {
                type: Number,
                default: 10
            },

        },
        methods: {
            scroll() {
                const step = timestamp => {
                    document.body.scrollTop -= 100;
                    if (document.body.scrollTop > 0) {
                        requestAnimationFrame(step)
                    }
                }
                requestAnimationFrame(step)
            }
        }
    };
</script>

<style lang="css" scoped>
    .goTop {
        width: 50px;
        height: 50px;
        background-color: #409bff;
        position: fixed;
    }
    .animated {
        transition: 1s
    }
</style>
