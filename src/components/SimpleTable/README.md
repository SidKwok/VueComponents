## SimpleTable

> table that can sort, pagination, searchText

## Goals

 * [x] Search
 * [x] Pagination
 * [x] Sort
 * [] Custom the functions you want, such as `search: false`
 * [] Set the default number of rows in a page.

## Noted

It has no style, so you can custom the style you want. The reason why I don't apply any style in it coz it's unnecessary. It's a functional table, not a fancy one.

## Usage

### Example

```html
<simple-table
    :options="options"
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

Include options, there is a `pagecount` being used to show amount of rows in one page.
