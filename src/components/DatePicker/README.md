# DatePicker

> as the name says

## Goals

 * [x] Pick the date
 * [x] Return the date, means `sync`
 * [] Change the country

## Noted

This component use [Flatpickr](https://chmln.github.io/flatpickr/) to create the datepicker, which is quite something, elegant and flat. But it means I have to use its stylesheet to beautify the component.

So you need to `install` it first:

```bash
npm install flatpickr
```

If you find out there is no style on it, feel free to change the `css` file path under the `<style>`.

## Usage

### Example

```html
<date-picker
    :date.sync="date"
    :options="options">
</date-picker>
```

### Default API

```javascript
props: {
    // you can check the documentation(https://chmln.github.io/flatpickr/)
    // to custom the options whatever you want
    // just don't mess up with onChange
    // coz i used it to update the date
    // i will find a better way to solve this :-(
    options: {
        type: Object,
        default() {
            return {};
        }
    },
    // send the date out
    // has to be twoWay binding
    // so it can pass the date out of the component
    date: {
        type: String,
        required: true,
        twoWay: true
    }
},
```
