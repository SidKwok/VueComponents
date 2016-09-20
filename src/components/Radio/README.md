# Radio

> As the name says

## Can be used! ✌️

## Goals

 * [x] Animation

## Noted

It should come with a group. You are supposed to choose a same name in one group so that the radio can find out which group it belongs to.

## Usage

### Example

```html
<radio :name.sync="picked" value="one"></radio>
<radio :name.sync="picked" value="two"></radio>
```

```javascript
data() {
    return {
        picked: 'one'
    }
}
```
### Default API

```javascript
props: {
    // the radio group it belongs
    name: {
        type: String,
        required: true,
        twoWay: true
    },
    // it's value
    value: {
        type: String,
        required: true
    },
    // size of radio
    size: {
        type: Number,
        default: 16
    },
},
```
