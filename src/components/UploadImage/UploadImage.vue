<template lang="html">
    <label class="uploadImage"
        :style="{
            backgroundImage: `url(${imgUrl})`
            }">
        <input
            type="file"
            accept="image/*"
            class="dn"
            @change="saveImage($event.target.files[0])"
        >
    </label>
</template>

<script>
    export default {
        data() {
            return {
                imgUrl: ''
            }
        },
        methods: {
            saveImage(file) {
                let img = new FileReader();
                img.readAsDataURL(file);
                img.onload = e => this.imgUrl = e.currentTarget.result;
            }
        }
    };
</script>

<style lang="css">
    .dn {
        display: none;
    }
    .uploadImage {
        display: block;
        width: 100px;
        height: 100px;
        border: 1px solid #000;
        margin: 0 auto;
    }
</style>
