# Aside

> Aside notification

## Can be used! ✌️

## Goals

 * [x] Slide in and out
 * [x] Click the blank space and out.
 * [x] Overlay should fade in and out. (need discussion)
 * [x] Choose right or left aside.

## Usage

### Example

```html
<aside
    :show.sync="show"
    title="yo im aside"
    :width="300"
    position="right"
>
    <h1>yoyo</h1>
    <p v-for="i in 10">what's up biatch!</p>
</aside>
```

### Default API

```javascript
props: {
    // has to be twoWay binding
    // it needs to be control in an out
    show: {
        type: Boolean,
        default: false,
        twoWay: true
    },
    // aside content's title
    title: {
        type: String,
        default: '',
    },
    // position of aside: left, right
    position: {
        type: String,
        default: 'left'
    },
    // set the width you want
    width: {
        type: Number,
        default: 350
    }
},
```
