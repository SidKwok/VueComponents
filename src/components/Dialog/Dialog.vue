<template lang="html">
    <div class="dialog" v-show="show" transition="fade">
        <div class="overlay" @click="close"></div>
        <div class="dialog-box" v-show="show"
            transition="zoom"
            :style="{
                width: `${width}px`,
                }">
            <div class="dialog-head">
                <button class="close" @click="close"></button>
                <p class="title">{{ title }}</p>
            </div>
            <div class="dialog-content">
                <slot><slot>
            </div>
            <div class="btn-group">
                <a href="javascript: void(0);"
                    :class="`dialog-${type}`"
                    @click="doNext"
                >
                    {{ okText }}
                </a>
                <a href="javascript: void(0);"
                    class="dialog-cancel"
                    v-if="showCancel"
                    @click="close"
                >
                    Cancel
                </a>
            </div>
        </div>
    </div>
</template>

<script>
    export default {
      data() {
          return {
          };
      },
      props: {
          // show the dialog or not
          // has to be twoWay binding
          // so you can control it in and out
          show: {
              type: Boolean,
              default: false,
              twoWay: true
          },
          // title above
          title: {
              type: String,
              required: true
          },
          // what kind of the dialog
          // info, success, confirm, warn, error
          type: {
              type: String,
              default: 'info'
          },
          // width of the center box
          width: {
              type: Number,
              default: 500
          },
      },
      computed: {
          showCancel() {
              return (this.type === 'confirm' || this.type === 'warn')
          },
          okText() {
              let text = '';
              switch (this.type) {
                  case 'confirm':
                  case 'warn':
                      text = 'confirm';
                      break;
                  case 'error':
                  case 'info':
                  case 'success':
                  default:
                      text = 'Ok'
                      break;
              }
              return text;
          }
      },
      methods: {
          doNext() {
              switch (this.type) {
                  case 'confirm':
                      this.$emit('confirm');
                      break;
                  case 'warn':
                      this.$emit('warn')
                      break;
              }
              // each button should be able to close dialog
              this.close();
          },
          close() {
              this.show = false;
          }
      },
    };
</script>

<style lang="css" scoped>
    .dialog {
        position: fixed;
        width: 100%;
        height: 100%;
        top: 0px;
        left: 0px;
    }
    .overlay {
        position: absolute;
        width: 100%;
        height: 100%;
        background-color: #000;
        opacity: .5;
        z-index: -1000;
    }
    .dialog-head {
        position: relative;
        padding: 20px;
        border-bottom: 1px solid #ded6db;
    }
    .dialog-head .close{
        background-color: rgba(17, 17, 17, 0.2);
        border: none;
        border-radius: 0 3px;
        cursor: pointer;
        display: inline-block;
        height: 24px;
        position: absolute;
        vertical-align: top;
        width: 24px;
        top: 0px;
        right: 0px;
    }
    .dialog-head .close::before {
        transform: rotate(45deg);
    }
    .dialog-head .close::after {
        transform: rotate(-45deg);
    }
    .dialog-head .close::before,
    .dialog-head .close::after {
        background-color: #fff;
        content: "";
        display: block;
        height: 2px;
        left: 50%;
        margin-left: -25%;
        margin-top: -1px;
        position: absolute;
        top: 50%;
        width: 50%;
    }
    .dialog-head .title {
        margin: 0;
        color: #222324;
        font-size: 24px;
    }
    .dialog-box {
        background-color: #eee;
        border-radius: 2px;
        margin: 10% auto;
    }
    .dialog-content {
        margin: 35px auto;
        width: 98%;
        text-align: center;
    }
    .btn-group {
        margin: 0px auto;
        padding-bottom: 20px;
        width: 98%;
        text-align: center;
    }
    .btn-group a {
        color: #000;
        border: #333 solid 1px;
        text-decoration: none;
        display: inline-block;
        border-radius: 2px;
        min-width: 80px;
        height: 30px;
        line-height: 30px;
        margin: 0px 10px;
    }
    .btn-group .dialog-info {
        background-color: #eee;
    }
    .btn-group .dialog-confirm {
        border-color: #42afe3;
        color: #42afe3;
    }
    .btn-group .dialog-success {
        border-color: #97cd76;
        color: #97cd76;
    }
    .btn-group .dialog-warn {
        border-color: #fce473;
        color: #fce473;
    }
    .btn-group .dialog-error {
        border-color: #ed6c63;
        color: #ed6c63;
    }
    .btn-group .dialog-cancel {
        background-color: #eee;
    }
    /*Animations*/
    .fade-transition {
        transition: all .3s;
    }
    .fade-enter, .fade-leave {
        opacity: 0;
    }

    .zoom-transition {
        animation-duration: .3s;
        animation-fill-mode: both;
    }
    .zoom-enter {
        animation-name: zoomIn;
    }

    @keyframes zoomIn {
        from, 20%, 40%, 60%, 80%, to {
            animation-timing-function: cubic-bezier(0.215, 0.610, 0.355, 1.000);
        }

        0% {
            opacity: 0;
            transform: scale3d(.3, .3, .3);
        }

        to {
            opacity: 1;
            transform: scale3d(1, 1, 1);
        }
    }

    .zoom-leave {
        animation-name: zoomOut;
    }
    @keyframes zoomOut {
        from {
            transform: scale3d(1, 1, 1);
        }

        to {
            opacity: 0;
            transform: scale3d(.3, .3, .3);
        }
    }
</style>
