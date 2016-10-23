<template lang="html">
    <div class="dropdown">
        <select v-model="list">
            <option v-for="option in options">{{ option }}</option>
        </select>
    </div>
</template>

<script>
export default {
    data() {
        return {}
    },
    props: {
        list: {
            type: Array,
            required: true,
            twoWay: true
        },
        options: {
            type: Array,
            required: true
        }
    }
}
</script>

<style lang="css">
</style>
