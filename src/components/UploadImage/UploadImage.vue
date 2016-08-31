<template lang="html">
    <div class="uploadImage-cover">
        <label v-el:image
            class="uploadImage"
            @dragenter.prevent.stop="dragenter"
            @dragleave.prevent.stop="dragleave"
            @dragover.prevent.stop
            @drop.prevent.stop="saveImage($event.dataTransfer.files[0])"
            :style="{
                backgroundImage: `url(${imgUrl})`,
                width: `${width}px`,
                height: `${height}px`
                }">
            <input
                type="file"
                accept="image/*"
                class="dn"
                @change="saveImage($event.target.files[0])"
            >
        </label>
        <p>
            {{ info }}
        </p>
    </div>
</template>

<script>
    export default {
        data() {
            return {
                imgUrl: ''
            }
        },
        props: {
            // default image
            // should be a url
            img: String,
            // send the formdata out,
            // so you can upload the image
            formdata: {
                required: true,
                twoWay: true
            },
            // limit of the image
            // KB
            limit: {
                type: Number,
                default: 40
            },
            // info below the image
            info: String,
            width: {
                type: Number,
                default: 100
            },
            height: {
                type: Number,
                default: 100
            }
        },
        methods: {
            dragenter() {
                this.$els.image.classList.add('red-line');
            },
            dragleave() {
                this.$els.image.classList.remove('red-line');
            },
            saveImage(file) {
                this.$els.image.classList.remove('red-line');
                if (file.size <= (this.limit * 1000)) {
                    this.formdata = file;
                    let img = new FileReader();
                    img.readAsDataURL(file);
                    img.onload = e => this.imgUrl = e.currentTarget.result;
                } else {
                    this.$emit('error')
                }
            }
        }
    };
</script>

<style lang="css" scoped>
    .dn {
        display: none;
    }
    .uploadImage-cover {
        position: relative;
        width: 150px;
        height: 150px;
        padding: 20px;
    }
    .uploadImage {
        display: block;
        background-size: 100px 100px;
        background-repeat: no-repeat;
        border: 1px solid #000;
        border-radius: 5px;
        margin: 20px auto;
    }
    .red-line {
        border-color: red;
    }
</style>
