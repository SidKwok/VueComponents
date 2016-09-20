## SimpleTable

> table that can sort, pagination, searchText

## Can be used! ✌️

## Goals

 * [x] Search
 * [x] Pagination
 * [x] Sort
 * [] Custom the functions you want, such as `search: false`
 * [x] Set the default number of rows in a page.

## Noted

It has no style, so you can custom the style you want. The reason why I don't apply any style in it coz it's unnecessary. It's a functional table, not a fancy one.

## Usage

### Example

```html
<simple-table
    :data="data"
    :titles="titles"
    :sortcols="sortcols"
    :pagecount="5"
></simple-table>
```

```js
options: {
    // titles name
    titles: [{name: 'date'}, {name: 'number'}],
    // the cols you need to sort
    sortCols: [true, true],
    // please ensure that that length of each row
    // is the same as titles' length
    data: [
        ['20160105', 8],
        ['20160203', 3],
        ['20160808', 1],
        ['20160301', 9],
        ['20160703', 5],
        ['20160105', 8],
        ['20160203', 3],
        ['20160808', 1],
        ['20160301', 9],
        ['20160703', 5],
        ['20160105', 8],
    ]
}
```

### Default API

```javascript
props: {
    // titles name
    titles: {
        type: Array,
        required: true
    },
    // the cols you need to sort
    sortcols: {
        type: Array,
        default() {
            return [];
        }
    },
    // please ensure that that length of each row
    // is the same as titles' length
    data: {
        type: Array,
        default() {
            return [];
        }
    },
    // show amount of rows in one page
    pagecount: {
        type: Number,
        default: 10
    }
},
```
