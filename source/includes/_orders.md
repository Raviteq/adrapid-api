# Orders

Orders are used to generate the banners (items) from a given template. Orders are long
running processes that their completion time depends on many factors, such as number
of items, complexity, image quality, etc.

AdRapid will run orders in an optimized parallel engine that will be able to quickly render the
results in typically less than one minute.

## Send Order

```javascript
var adrapid = require('adrapid')({
  url: 'http://api.adrapid.com',
  key: 'my API key',
  token: 'my secret token'
});

var order = {
  "templateId":         "qual3097a002fdaeeb02a79e877bb9bda7e502ae",
  "formats":            "300x250,980x240",
  "text_field1_1":      "Sony Xperia Z3",
  "text_field1_2":      "The brand new",
  "text_field1_3":      "city mobile",
  "text_field1_7":      "Valid until 14/12/14",
  "text_sign2_1":       "$199",
  "text_sign1_2":       "Org. price $399",
  "text_sign1_4":       "NOW!",
  "text_sign1_3":       "Buy now!",
  "text_sign1_1":       "XPERIA Z3",
  "text_field1_4":      "Waterproof",
  "text_field1_5":      "5.2-inch 4K screen",
  "text_field1_6":      "920 standby hours",
  "img_1":              "http://my-site.com/img/product.png",
  "img_2":              "http://my-site.com/img/logo.png",
  "img_3":              "http://my-site.com/img/background.jpg",
  "color_background1":  "#3399ff",
  "color_sign1":        "#ff6600",
  "color_text_field1":  "#333333",
  "color_text_sign1":   "#3344ff",
  "client_data":        "my own ID",
  "callback_url":       "http://my-site.com/order_callback.php"
}

adrapid.sendOrder(order).then(function(orderId){
  console.log('order sent with id:', orderId);
}, function(err){
  console.error('order failed', err);
});
```

```shell
curl "http://api.adrapid.com/orders"
  -H "Authorization: my API key"
  -H "Content-Type:application/json" 
  -d @order.json 
```

> example order data

```json
{
  "templateId":         "qual3097a002fdaeeb02a79e877bb9bda7e502ae",
  "formats":            "300x250,980x240",
  "text_field1_1":      "Sony Xperia Z3",
  "text_field1_2":      "The brand new",
  "text_field1_3":      "city mobile",
  "text_field1_7":      "Valid until 14\/12\/14",
  "text_sign2_1":       "$199",
  "text_sign1_2":       "Org. price $399",
  "text_sign1_4":       "NOW!",
  "text_sign1_3":       "Buy now!",
  "text_sign1_1":       "XPERIA Z3",
  "text_field1_4":      "Waterproof",
  "text_field1_5":      "5.2-inch 4K screen",
  "text_field1_6":      "920 standby hours",
  "img_1":              "http://my-site.com/img/product.png",
  "img_2":              "http://my-site.com/img/logo.png",
  "img_3":              "http://my-site.com/img/background.jpg",
  "color_background1":  "#3399ff",
  "color_sign1":        "#ff6600",
  "color_text_field1":  "#333333",
  "color_text_sign1":   "#3344ff",
  "callback_url":       "http://my-site.com/order_callback.php",
  "client_data":        "my own ID"
}
```

This endpoint posts an order to generate a set of banners for a given template using the supplied order data.

### HTTP Request

`POST http://api.adrapid.com/orders`


Returns an `orderId` that can be used by other API:s to retrieve order status and events.


### Mandatory Body parameters

Parameter | Description
--------- | -----------
templateId | The ID of template to use for the order.
formats | The requested formats, at least one valid ad format is required.


The required fields for the ad content is supplied by the `template rules` method. No
validation is required for text fields. However, produced ads will look empty if
fields are missing, and texts will be clipped or downsized if they exceed the `max_length` limit.

Invalid or missing colors and images are simply ignored, and will not cause an error.

<aside class="success">
Hint: use the Events API to retrieve real time status of your order!
</aside>

### Sending images

Images can be sent as either an *URL*, as *binary data* (ie. standard HTTP POST), or as a *base64-encoded* string. It is also possible to use a *mediaId* of a previously uploaded media item to reuse it.

> All these color examples are valid:

```json
{
    "color_background1": "#3399ff",
    "color_sign1":       "hsl(200,10,20)",
    "color_text_field1": "rgba(100, 250, 0, 0.55)",
    "color_text_sign1":  "cmyk(1, 2, 3, 4)"
}
```
### Sending colors

Colors can be send in HEX, rgb(a), CMYK or HSL.

### Setting banner formats

Order formats are determined by the `formats` string. The formats string should contain a set of
order items, separated by commas.

<aside class="success">
Hint: use the `formats` API to get a list of available formats.
</aside>

### Include custom data and returning via a callback url

Order requests may contain own `client_data`, which if included will be passed through
the order and returned in the request to given `callback_url`.

`client_data`, may contain any string, such as any valid JSON object. When the order is completed,
a request is made to the url specified in the `callback_url`, containing the order ID as well as
the `client_data` string.


## Get order

```javascript
var adrapid = require('adrapid')({
  url: 'http://api.adrapid.com/',
  key: 'my API key',
  token: 'my secret token'
});

adrapid.getOrder(orderId).then(function(order){
  console.log(order)
}, function(err){
  console.error(err);
});
```

```shell
curl "http://api.adrapid.com/orders/$MY_ORDER_ID"
  -H "Authorization: my API key"
```

> The above command returns JSON structured like this:

```json
{
    "status": "rendering",
    "items": [
    {
      "id":     "1234",
      "type":   "banner",
      "format": "980x240",
      "url":    "http://orders.adrapid.com/:orderId/:itemId"
    }
  ]
}
```

Gets the details of an order. Useful to get the status of a given order as well
as the urls for the results. The urls are short lived and should be used by the
client of the API just to copy them to a proper server. The contents of the order
urls are only guaranteed to exist 24 hours after the order has been executed.

`GET http://api.adrapid.com/orders/:id`

### URL Parameters

Parameter |  Description
--------- | -------------
id        | id of the order we want to retrieve its data.



### Get order data
Retreives the values (texts, colors and images) used in a certain order.

`GET http://api.adrapid.com/orders/:id/data`


## Get embed code

<aside class="warning">Currently not implemented in API v2</aside>

```javascript
var adrapid = require('adrapid')({
  url: 'http://api.adrapid.com/',
  key: 'my API key',
  token: 'my secret token'
});

adrapid.getPreview(itemId).then(function(result){
  document.body.appendChild(result.preview);
}, function(err){
  console.error(err);
});
```

```shell
curl "http://api.adrapid.com/get_item_content/$MY_ITEM_ID"
  -H "Authorization: my API key"
```

> The above command returns an JSON array, the property `preview` contains HTML for the selected order item.

```html
TODO
```

Get the embed HTML for an order item. Since different ad types requires different embed code, we provide this method for easily getting the content of an order item.

`GET http://api.adrapid.com/get_item_content/:item_id`

### URL Parameters

Parameter |  Description
--------- | -------------
item_id   | id of the order item we want to retrieve embed code for.
