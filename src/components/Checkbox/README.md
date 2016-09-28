# Checkbox

> As the name says.

## Can be used! ✌️

## Goals

 * [x] Animation

## Noted

You are supposed to bind your Checkboxes with a single group, so that you can access all your checked value in the array and send them back to backend.

## Usage

### Example

```html
<Checkbox value="one" :group.sync="list">hey man</Checkbox>
<Checkbox value="two" :group.sync="list"></Checkbox>
```

```javascript
...
list: []
...
```
### Default API

```javascript
props: {
    // value of the checkbox
    value: {
        type: String,
        required: true
    },
    // the group it is belonged to
    // has to be two way binding
    group: {
        required: true,
        twoWay: true
    },
    // show the text if exists
    text: {
        type: String,
        default: ''
    }
},
```
