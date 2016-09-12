# Upload

> Upload all kinds of file(may be not all)

## Goals

 * [x] Dragable.
 * [x] Set type of the files
 * [x] Send the `formData` through twoWay binding

## Noted
 This component is supposed to work with some `ajax` way to upload the `FormData` it gets. If you use `vue-resource`, you should do this:
 ```javascript
 this.$http.get(
     '/upload/file',
     formData, // this is form by Upload
 ).then(response => console.log(response))
 .catch(errMsg => console.log(errMsg));
 ```
 The reason why I didn't enclosure the `ajax` function in the component is that you can do lots tons of things outside Upload such as `progress` and some responsive functions. It seems a more flexible way to manage the data.

## Usage

### Example

```html
<upload
    :form-data.sync="formData"
    :suffix-group="['png', 'jpeg']"
    info="yoyo"
    @error="dosth"
><upload>
```
### Default API

```javascript
props: {
    // suffix of the file.
    // but it can't really tell
    // if the type is absolutely correct.
    // That's because dudes can change the
    // suffix of the file and js has no
    // way to find out.
    suffixGroup: {
        type: Array,
        default() {
            return ['*'];
        }
    },
    // default image
    // should be a url
    img: String,
    // send the formdata out,
    // so you can upload the image
    formData: {
        required: true,
        twoWay: true
    },
    // limit of the image
    // KB
    limit: {
        type: Number,
        default: 40
    },
    info: String,
    width: {
        type: Number,
        default: 100
    },
    height: {
        type: Number,
        default: 100
    }
},
```
