# awesome-react-gallery

> Gallery component for S3 image directory

[![NPM](https://img.shields.io/npm/v/awesome-react-gallery.svg)](https://www.npmjs.com/package/awesome-react-gallery) [![JavaScript Style Guide](https://img.shields.io/badge/code_style-standard-brightgreen.svg)](https://standardjs.com)

## Install

```bash
npm install --save upgrad/react-image-gallery
```

## Usage

```jsx
import React, { Component } from "react";
import Gallery from "awesome-react-gallery";

class Example extends Component {
  constructor() {
    this.state = {
      showGallery: true
    };
    this.config = {
      server: "http://localhost:3000/gallery",
      style: {
        width: 60,
        align: "left"
      },
      s3: {
        bucket: "xxxx-xxxx-xxxx",
        path: "XXXXX/XXXX/XXXXX"
      },
      cdn: "XXXXX/XXXX/XXXXX"
  }

  onImageReceive = data => {
    this.setState({
      ...this.state,
      showGallery: false,
      image: data.imageUrl
    });
  };

  render() {
    return (
      <div>
        <img src={this.state.image} />
        {this.state.showGallery ? (
          <Gallery onClose={this.onImageReceive} config={this.config} />
        ) : null}
      </div>
    );
  }
}
```

## Config

| Key  | Purpose |
| ------------- | ------------- |
| server  | A url for the server APIs. Refer the middleware [express-s3-image-resources](https://github.com/upgrad/express-s3-image-resources/) to know how to configure the APIs for this gallery |
| s3.bucket  | A bucket name from which images are to be rendered by awesome gallery  |
| s3.path  | A path in the bucket from which the images are to be fetched and rendered |
| cdn  | A path to the cdn which needs to suffixed along with the image that gets selected  |
| style  | A object which contains normal UI options like width and alignment of gallery component  |
| uploadRestrictions  | Set of rules for image | 


### uploadRestrictions

| Key  | parameters | examples |
| ------------- | ------------- | ------------- |
| dimensions | width , height | ```{"width": 1600, "height": 900 }```|
| aspectRatio | [ '1:1', '4:3', '5:4', '3:2', '16:10', '16:9', '21:9', '32:9' ] | "16:9"|
| errorAllowed | 1-100 | 50
| orientation | portrait, landscape | portrait (default value)



The s3 Path and s3 Bucket parameters will be used on server side by the [express-s3-image-resources middleware](https://github.com/upgrad/express-s3-image-resources/) to fetch the images from aws. This NPM doesn't require you to pass any aws credentials.

## License

MIT © [upgrad](https://github.com/upgrad)
