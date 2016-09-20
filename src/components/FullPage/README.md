# FullPage

> scroll the pages

## Can be used! ✌️

## Goals

 * [x] Full page scroll
 * [x] A toolbox that can assess any pages
 * [x] Animations
 * [x] Use `<slot>` to contain pages
 * [x] events: enter

## Noted

For activate this component, you should send the `slot` in the component. You can edit everything in slot and the scroll is just fine. But remember this is a component for the full page, which means it is better used as the introduction page. So don't put too much logic in your introduction page, it may ruin the whole page.

Every page's `position` is `relative`, so you may consider well before you write your code down.

Every time enters a page, it will send an event which contains `dom` of current page and previous page like `test(currentPage, previousPage)`.

## Usage

### Example
```html
<full-page :pages="3" @enter="dosth">
    <div slot="page-1" style="background-color: rgb(27, 188, 155);width: 100%;height: 100%;"></div>
    <div slot="page-2" style="background-color: rgb(255, 153, 0);width: 100%;height: 100%;"></div>
    <div slot="page-3" style="background-color: rgb(123, 170, 190);width: 100%;height: 100%;"></div>
</full-page>
```

### Default API
```javascript
props: {
    // how many pages you want to show
    pages: {
        type: Number,
        required: true
    },
},
```
