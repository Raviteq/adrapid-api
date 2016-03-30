# Templates

Templates are the basic structure from which a banner (also called *item*) can be generated.
You start by getting the templates available for the current user, and
later on you can send orders based on a given template.

## Get templates

```javascript
var adrapid = require('adrapid')({
  url: 'http://platform.adrapid.com/api/',
  key: 'my API key',
  token: 'my secret token'
});

adrapid.getTemplates().then(function(templates){

}, function(err){
  console.error('Error getting templates', err);
});

```

> Example result of calling the get templates method

```json
[{
  "id": "qual3097a002fdaeeb02a79e877bb9bda7e502ae",
  "name": "AdRapid product 1",
  "identifier": "adrapid-product00001",
  "thumbnail": "http://adrapid.com/img/template_thumbnails/adrapid_product1_videothumbnail.jpg"
},
{
  "id": "snowwq97a0l2fdabeb02a79e877bb9bda7e502ae",
  "name": "Product snow",
  "identifier": "mxm-product_snow",
  "thumbnail": "http://adrapid.com/img/template_thumbnails/mxm-product_snow_videothumbnail.jpg"
},
{
  "id": "service-image_xbeb02a79e877bb9bda7e502ae",
  "name": "Service image",
  "identifier": "mxm-service_image",
  "thumbnail": "http://adrapid.com/img/template_thumbnails/mxm-service_image.jpg"
}]
```

Gets available templates for a given client.

### HTTP Request

`GET http://api.adrapid.com/templates`


## Getting rules for template

Get the rules for a given template.

### HTTP Request

`GET http://api.adrapid.com/templates/:id/rules`


### URL parameters

Parameter | Description
--------- | -----------
:id | The ID of template.


## Getting available formats for template

Get the available formats for a given template.

### HTTP Request

`GET http://api.adrapid.com/templates/:id/formats`

### URL parameters

Parameter | Description
--------- | -----------
id | The ID of template.


## Getting dummy content for template

> Example fields:

```json
{
  "text_field1_1": "text_field1_1",
  "text_field1_2": "text_field1_2",
  "text_field1_3": "text_field1_3",
  "text_field1_4": "text_field1_4",
  "text_field1_8": "text_field1_8",
  "tex,t_field1_9": "text_field1_9",
  "text_field1_10": "text_field1_10",
  "text_sign1_1": "text_sign1_1",
  "text_sign1_2": "text_sign1_2",
  "text_sign1_3": "text_sign1_3",
  "text_sign1_4": "text_sign1_4",
  "text_sign2_1": "text_sign2_1"
}
```

Returns an array of dummy content for the template's fields.
Primarily intended for understanding the API/order structure or as dummy values
for a template preview.

### HTTP Request

`GET http://api.adrapid.com/templates/:id/dummy`


### URL parameters

Parameter | Description
--------- | -----------
id | The ID of template.


## Retrieving template preview

It is also possible to retrieve a quick preview of a template before actually sending
a time consuming order.

Returns a html preview.

<aside class="warning">Currently autentication is not implemented.</aside>

### HTTP Request

`GET http://api.adrapid.com/templates/:id/preview`

### URL parameters

Parameter | Description
--------- | -----------
id | The ID of template.

