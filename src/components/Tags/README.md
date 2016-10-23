# Tags

> Multiple tags

## Can be used! ✌️

## Goals

 * [x] Different color for different meaning.
 * [x] Turn to dots when it has too many tags.
 * [] Hover effect.

## Usage
You should send the value and also the colors in this component so that it can show the exact tag with proper color.

### Example
```html
<tags :tags="tags" :limits="2"></tags>
```

### Default API
```javascript
props: {
    // {value: 'great', text: '#8a89e0', bg: '#e9e8f6'}
    // each tag should has the values above
    tags: {
        type: Array,
        required: true
    },
    // if the number of tags is more than this value
    // tags will turn to dots.
    limits: {
        type: Number,
        default: 9999
    }
}
```
