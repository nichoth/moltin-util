# moltin util

Tool for working with the Moltin API. Plus, promises!


## install

    $ npm install moltin-util


## example

Upload an image:

```js
var MoltinUtil = require('moltin-util');

var client = MoltinUtil({
  publicId: process.env.PUBLIC_ID,
  secretKey: process.env.SECRET_KEY
});

client.fetchImage('http://example.com/image.jpg')
  .then(util.resize.bind(util, 600))
  // opts for api: https://docs.moltin.com/images/
  .then(util.createImage.bind(util, {
    name: 'example.jpg'
  }))
  .then(resp => console.log(resp.body))
  .catch(err => console.log('error', err))
;
```

Get a list of products:

```js
require('dotenv').config();
var client = require('moltin-util')({
  publicId: process.env.PUBLIC_ID,
  secretKey: process.env.SECRET_KEY
});

// call `got` with some defaults
client.request(util.endpoints.PRODUCTS)
  .then(resp => console.log(resp))
  .catch(err => console.log('err', err))
;
```

Create a product. Takes an optional array of images. 

```js
require('dotenv').config();
var client = require('moltin-util')({
  publicId: process.env.PUBLIC_ID,
  secretKey: process.env.SECRET_KEY
});

var product = {
  title: 'Bulk Glass Eye Charms',
  price: 30,
  description: 'Eye charms',
  slug: 'bulk-glass-eye-charms',
  sku: 'bulk-glass-eye-charms',
  status: 1,
  category: '123',
  stock_level: '1',
  stock_status: 1,
  requires_shipping: 1,
  catalog_only: 0,
  tax_band: '123'
};

var images = ['http://example.com/image.jpg'];

client.createProduct(product, images)
  .then(res => console.log(res.product, res.images))
  .catch(err => console.log(err, err.response.body))
;
```
