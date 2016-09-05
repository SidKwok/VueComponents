# FullPage

> scroll the pages

## Goals

 * [x] Full page scroll
 * [x] A toolbox that can assess any pages
 * [x] Animations
 * [x] Use `<slot>` to contain pages
 * [] events: enter

## Noted

For activate this component, you should send the `slot` in the component. You can edit everything in slot and the scroll is just fine. But remember this is a component for the full page, which means it is better used as the introduction page. So don't put too much logic in your introduction page, it may ruin the whole page.

## Usage

### Example
```html
<full-page :pages="3">
    <template slot="page-1">1</template>
    <template slot="page-2">2</template>
    <template slot="page-3">3</template>
</full-page>
```

### Default API
