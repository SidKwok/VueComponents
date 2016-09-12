<template lang="html">
    <div class="uploadCover">
        <label v-el:upload
            class="upload"
            @dragenter.prevent.stop="dragenter"
            @dragleave.prevent.stop="dragleave"
            @dragover.prevent.stop
            @drop.prevent.stop="save($event.dataTransfer.files[0])"
            :style="{
                backgroundImage: `url(${imgUrl ? imgUrl : img})`,
                width: `${width}px`,
                height: `${height}px`
                }">
            <input
                type="file"
                class="dn"
                @change="save($event.target.files[0])"
            >
        </label>
        <p class="info">
            {{ info }}
        </p>
    </div>
</template>

<script>
    export default {
        data() {
            return {
                imgUrl: ''
            };
        },
        props: {
            // suffix of the file.
            // but it can't really tell
            // if the type is absolutely correct.
            // That's because dudes can change the
            // suffix of the file and js has no
            // way to find out.
            suffixGroup: {
                type: Array,
                default() {
                    return ['*'];
                }
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
                this.$els.upload.classList.add('red-line');
            },
            dragleave() {
                this.$els.upload.classList.remove('red-line');
            },
            save(file) {
                this.$els.upload.classList.remove('red-line');
                let size = file.size;
                let type = file.type.split('/')[0];
                let name = file.name;
                let suffix = name.slice(name.lastIndexOf('.') + 1, name.length);

                // detect size first
                if (size <= this.limit * 1000) {
                    // detect suffix
                    if (this.suffixGroup[0] === '*' || this.suffixGroup.includes(suffix)) {
                        this.formData = file;
                        // detect type
                        if (type === 'image') {
                            let img = new FileReader();
                            img.onload = e => this.imgUrl = e.currentTarget.result;
                            img.readAsDataURL(file);
                        } else {

                        }
                    } else {
                        this.$emit('error', 'wrongFile');
                    }
                } else {
                    this.$emit('error', 'overSize');
                }
            }
        }
    };
</script>

<style lang="css" scoped>
    .dn {
        display: none;
    }
    .uploadCover {
        position: relative;
        width: 150px;
        height: 150px;
        padding: 20px;
    }
    .upload {
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
    .info {
        text-align: center;
        margin: 0 auto;
    }
</style>
