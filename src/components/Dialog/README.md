# Dialog

> Dialog that will popup, mainly used to show some information.

## Can be used! ✌️

## Goals

 * [x] Popup
 * [x] Animations
 * [x] Types: info, success, confirm, warn
 * [x] It should have yesCallback and cancelCallback (use event)
 * [x] Use `<slot>` to contain the content outside
 * [x] Title
 * [] Can do multiple operation in a Dialog, such like success or fail after confirm.  

## Noted

 * Only `confirm` and `warn` type have callback event.
 * If you need to change the text of the buttons, feel free to change it in the component.

## Usage

### Example

```html
<dialog v-show="show"
    title="yoyoyo"
    type="success"
    :width="500"
    @confirm="doConfirm"
    @warn="doWarn"
>
    <h1>hey you</h1>
    <p>
        Jesse Pinkmen is in the house!
    </p>
</dialog>
```

```javascript
methods: {
    dosth() {
        this.show = !this.show;
    },
    doConfirm() {
        console.log('yo im confirm')
    },
    doWarn() {
        console.log('yo warn me for what?? biatch!')
    }
}
```

### Default API
```javascript
props: {
    type: {
        type: String,
        default: 'normal' // success, fail, warn, confirm
    },
    title: String,
    normalText: {
        type: String,
        default: '保存'
    },
    warnText: {
        type: String,
        default: '确认'
    },
    confirmText: {
        type: String,
        default: '确认'
    },
    cancelText: {
        type: String,
        default: '取消'
    },
    btnPos: {
        type: String,
        default: 'middle'
    },
    width: {
        type: Number,
        default: 400
    },
    showNormal: {
        type: Boolean,
        default: true
    }
}
```
