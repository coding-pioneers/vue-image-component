# vue-image-component

A Vue component to lazy load and display images.

## Installation
```
npm install vue-image-component --save
```

### Setup
```javascript
// in app.js
import Vue from 'vue';
Vue.component('vue-img', require('vue-image-component'));
```

### Usage
Here is an example with the minimum setup:

```html
<vue-img :full="https://example.com/myImage.png"><vue-img>
```

This will render an image with a spinner showing up while the image is loading.
Alternatively you can pass a small preview image with low quality via the <strong>preview</strong>-Property:

```html
<vue-img full="https://example.com/myImage.png"
         preview="https://example.com/myPreviewImage.png">
<vue-img>
```

When passing an preview image the component uses <em>progressive image loading</em>. If the image is successfully
loaded it will scale in.

## Available properties

The following properties are available: 

name        | required | type   | default   |description
:---        | :---:    | ---    | ---       |---
full        | x        | string | -         | The image to display. 
preview     |          | string | ''        | The image preview to use for `progressive image loading
alt         |          | string | ''        | The image alternate text.
width       |          | string | '120px'   | The image width.
height      |          | string | 'auto'    | The image height.
spinner-size|          | string | '64px'    | The spinner size.
css         |          | object | {}        | Optional css for the image container.
link        |          | string | ''        | A link where the image should link to.
data-src-set|          | string | ''        | The img data src set. **Experimental**
data-sizes  |          | string | ''        | The img data sizes. **Experimental**

