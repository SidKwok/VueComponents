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
 * I remove `show.sync` to make sure ~props down, events up~, so you need to use `v-show` or `v-if`. But `show` is still remained to trigger animation.

## Usage

### Example

```html
<dialog v-show="show"
    :show="show"
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
```
