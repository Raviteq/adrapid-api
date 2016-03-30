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
  "templateId": "qual3097a002fdaeeb02a79e877bb9bda7e502ae",
  "formats": "banner_300x250,banner_300x60,banner_980x240", "text_field1_1": "Sony Xperia Z3",
  "text_field1_2": "The brand new",
  "text_field1_3": "city mobile",
  "text_field1_7": "Valid until 14\/12\/14", "text_sign2_1": "$199",
  "text_sign1_2": "Org. price $399",
  "text_sign1_4": "NOW!",
  "text_sign1_3": "Buy now!",
  "text_sign1_1": "XPERIA Z3",
  "text_field1_4": "Waterproof",
  "text_field1_5": "5.2-inch 4K screen",
  "text_field1_6": "920 standby hours",
  "img_1": "http://my-site.com/img/product.png",
  "img_2": "http://my-site.com/img/logo.png",
  "img_3": "http://my-site.com/img/background.jpg", "color_background1": "#3399ff",
  "color_sign1": "#ff6600",
  "color_text_field1": "#333333",
  "color_text_sign1": "#3344ff",
  "client_data": "my own ID",
  "callback_url": "http://my-site.com/order_callback.php"
}

adrapid.sendOrder(order).then(function(orderId){
  console.log('order sent with id:', orderId);
}, function(err){
  console.error('order failed', err);
});
```

```shell
curl -d @order.json --header "Content-Type:application/json" "http://api.adrapid.com/orders"
  -H "Authorization: meowmeowmeow"
```

This endpoint posts an order to generate a set of banners based on a given template data.

### HTTP Request

`POST http://api.adrapid.com/orders`

Returns an order ID that can be used by other APIs to retrieve order status and events.


### Mandatory Body parameters

Parameter | Description
--------- | -----------
templateId | The ID of template to use for the order.

<aside class="success">
Hint: use the Events API to retrieve real time status of your order!
</aside>

### Sending images

Images can be sent as either a *URL*, raw binary data (ie. as standard "HTTP post"), or as a *base64-encoded* string.

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

Colors can be sent in HEX, rgb(a), CMYK or HSL.


### Setting banner/video formats for order

Order formats are determined by the string formats. The formats string should contain a set of
order items, separated by commas. Each item is named by its format, separated by an underscore,
followed by the size or identifier.

For example banner_320x160 and video_horizontal_15s ar valid formats. Some formats string examples:

`banner_980x240,banner_300x1050:google_adwords,video_horizontal_15s`

Available formats for a given template could be retrieved using the *get template formats* API.

### Include custom data and returning via a callback url

Order requests may contain own `client_data`, which if included will be passed through
the order and returned in the request to given `callback_url`.

`client_data`, may contain any string, such as any valid an json object. When the order is completed,
a request is made to the url specified in the `callback_url`, containing the order ID as well as
the `client_data` string.

## Get order

```javascript
var adrapid = require('adrapid')({
  url: 'http://platform.adrapid.com/api/',
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
  -H "Authorization: meowmeowmeow"
```

> The above command returns JSON structured like this:

```json
{
    "status": "rendering"
}
```

Gets the details of an order. Useful to get the status of a given order.

`GET http://api.adrapid.com/orders/:id`

### URL Parameters

Parameter |  Description
--------- | -------------
id        | id of the order we want to retrieve its data.

