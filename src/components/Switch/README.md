# Switch

> A Switch component

## Can be used! ✌️

## Goals

 * [x] Switch between `true` and `false`.
 * [x] Animation.
 * [] Need a tag name.
 * [x] Some unchangable switch prefer be gray

## Noted

Change the width and height whatever you like, but in my opinion, the default may have the best experience.

## Usage

### Example

```html
<switch
    :checked.sync="checked"
    :disabled="false"
></switch>
```

### Default API

```javascript
props: {
    // need twoWay binding to
    // send the value outside
    checked: {
        type: Boolean,
        default: false,
        twoWay: true
    },
    // disabled switch
    disabled: {
        type: Boolean,
        default: false
    },
    // they belong to the bar
    width: {
        type: Number,
        default: 34,
    },
    height: {
        type: Number,
        default: 14
    }
},
```
