# Toast

> Toast that you need to popup

## Goals

 * [x] four basic kind of notification (marked with color)
 * [x] timer to close the notification
 * [x] animations
 * [] more options of animation
 * [] custom size
 * [] custom location
 * [] multiple toasts 

## Usage

### Example

```html
<notification
    :show.sync="show"
    animation="bounceRight"
    type="normal"
    :expire="10000"
    :width="200"
    :height="100"
>
    Vue is gas!
</notification>
```
### Default API

```js
props: {
    // show the notification or not,
    // has to be twoWay binding,
    // ensure that it can be control in and out
    show: {
        type: Boolean,
        default: false,
        twoWay: false
    },
    // notification type: normal, success, warn, fail
    type: {
        type: String,
        default: 'normal'
    },
    // animation type: bounceLeft, bounceRight
    animation: {
        type: String,
        default: 'bounceRight'
    },
    // expire time
    expire: {
        type: Number,
        default: 10000
    },
    width: {
        type: Number,
        default: 200
    },
    height: {
        type: Number,
        default: 100
    },
},
```
