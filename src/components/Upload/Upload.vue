<template lang="html">
    <div class="uploadCover">
        <label v-el:upload
            class="upload"
            @dragenter.prevent.stop="dragenter"
            @dragleave.prevent.stop="dragleave"
            @dragover.prevent.stop
            @drop.prevent.stop="save($event.dataTransfer.files[0])"
            :style="{
                backgroundImage: `url(${imgUrl})`,
                width: `${width}px`,
                height: `${height}px`
                }">
            <input
                type="file"
                accept="image/*"
                class="dn"
                @change="save($event.target.files[0])"
            >
        </label>
        <p>
            {{ info }}
        </p>
    </div>
</template>

<script>
    export default {
        props: {
            // two kind of file
            // actual file and image
            fileType: {
                type: String,
                default: 'file'
            },
            // default image
            // should be a url
            img: String,
            // send the formdata out,
            // so you can upload the image
            formData: {
                required: true,
                twoWay: true
            },
            // limit of the image
            // KB
            limit: {
                type: Number,
                default: 40
            },
        },
        methods: {
            dragenter() {
                this.$els.file.classList.add('red-line');
            },
            dragleave() {
                this.$els.file.classList.remove('red-line');
            },
            saveImage(file) {
                this.$els.file.classList.remove('red-line');
                if (file.size <= (this.limit * 1000)) {
                    this.formData = file;
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

<style lang="css">
</style>
