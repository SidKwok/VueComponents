<template lang="html">
    <ul>
        <li v-for="i in counts">{{ i + 1 }}</li>
    </ul>
</template>

<script>
    export default {
        data() {
            return {
                currentPage: 1
            }
        },
        props: {
            // all pages
            counts: {
                type: Number,
                required: true
            },
        }
    };
</script>

<style lang="css" scoped>
</style>
