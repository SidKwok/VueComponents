# UploadImage

> Upload image through formdata

## Goals

 * [x] Dragable.
 * [x] Show image if needs.

## Noted

You may need to set a error callback to catch the error(only limit error).
And you should set a twoWay binding to get the formdata, this component is mainly used to upload image.
To upload this image, you can use `vue-resource`, `fetch`, or simple `xhr`.

## Usage

### Example

```html
<upload-image
    :limit="100"
    :formdata.sync="formdata"
    info="yoyoyo"
    @error="dosth"
></upload-image>
```
### Default API

```javascript
props: {
    // default image
    // should be a url
    img: String,
    // send the formdata out,
    // so you can upload the image
    formdata: {
        required: true,
        twoWay: true
    },
    // limit of the image
    // KB
    limit: {
        type: Number,
        default: 40
    },
    // info below the image
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
