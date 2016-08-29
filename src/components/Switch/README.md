# Switch

> A Switch component

## Goals

 * [x] Switch between `true` and `false`.
 * [x] Animation.
 * [] Need a tag name.
 * [] Some unchangable switch prefer be gray

## Usage

### Example

```html
<switch
    :checked.sync="checked"
    :height="20"
    :width="50"
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
    // TODO!!!
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
