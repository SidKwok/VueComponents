# Pager

> As name says

## Can be used! ✌️

## Goals

 * [x] Event: update

## Noted
When you update the page size of the current page, it will send the same event called `update` with an `Object` `{page: 10, limit: 5}`.

## Usage

### Example

```html
<pager @update="updatePageSync"></pager>
```


### Default API
```javascript
props: {
    count: Number
}
```
