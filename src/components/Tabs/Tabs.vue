<template lang="html">
    <div class="tabs">
        <div class="tabs-header">
            <ul>
                <li v-for="title in titles">
                    <p>
                        {{ title }}
                    </p>
                </li>
            </ul>
        </div>
        <slot v-for="title in titles" :name="title"></slot>
    </div>
</template>

<script>
    export default {
        props: {
            // every title of the tabs
            // each title should be a {String}
            titles: {
                type: Array,
                required: true
            },
            width: {
                type: Number,
                default: 800
            },
            height: {
                type: Number,
                default: 600
            }
        }
    };
</script>

<style lang="css" scoped>
</style>
