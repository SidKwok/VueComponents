<template lang="html">
    <div class="tabs">
        <div class="tabs-wrapper">
            <div class="tabs-title">
                <div v-for="tab in titles"
                    @click="switchTab(tab)"
                    class="tab-item"
                    :class="{ 'selected':  (activeTab === tab) }"
                >
                    {{ tab }}
                </div>
            </div>
        </div>
    </div>
</template>

<script>
    export default {
        data() {
            return {
                activeTab: '',
            }
        },
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
        },
        methods: {
            switchTab(tab) {
                this.activeTab = tab;
            }
        }
    };
</script>

<style lang="css" scoped>
</style>
