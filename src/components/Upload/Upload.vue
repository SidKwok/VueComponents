<template lang="html">
    <div class="Upload">

    </div>
</template>

<script>
    export default {
        // two kind of file
        // actual file and image
        type: {
            type: String,
            default: 'file'
        },
        // limits of the file
        limits: {
            type: Number,
            default: 40000
        }
    };
</script>

<style lang="css">
</style>
