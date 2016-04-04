# Templates

Templates are the basic structure from which a banner or other type of
supported output media(also called *item*) can be generated.
You start by getting the all templates available for the current user, then select the
proper one as well as its rules and supported formats and finally you can you can
send orders based on the given template.

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

> Example result of calling the get template rules method

```json
{
   "id": "6066cd7b8712507a5b0d547aa64c370a91ac3f91",
   "name":"demo-phones",
   "formats": [
      "120x600",
      "160x600",
      "200x200",
      "240x400"
   ],
   "fields":[
      {
         "name":"text_field1_1",
         "label":"Product name",
         "type": "text",
         "max_length":20,
         "default":"AdRapid Phone"
      },
      {
         "name":"text_sign2_1",
         "label":"Price",
         "type": "text",
         "max_length":6,
         "default":"$399"
      },
      {
         "name":"img_1",
         "label":"Product image",
         "type": "image",
         "default":"http:\/\/platform.adrapid.com\/uploads\/client_uploads\/demo\/img\/b73f2d_ebf9_phone1024x1024.png"
      },
      {
         "name":"img_2",
         "label":"Product logo",
         "type": "image",
         "default":"http:\/\/platform.adrapid.com\/cache\/dummy_default\/logos-demo-mobile_pads\/adrapid_white.png"
      },
      {
         "name":"color_background1",
         "label":"Background color",
         "type": "color",
         "default":"#b8594c"
      },
      {
         "name":"color_texts",
         "label":"Text color",
         "type": "color",
         "default":"#ffffff"
      }
   ]
}
```

Get the rules for a given template. The rules of a template defines which
datatypes are allowed for every field available in the template, as well as
which are the supported output formats.

The following table shows the available field types:

type | Description
--------- | -----------
text | A string of text of a maximum length
image | A URL specifying a image
color | A valid color specification

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


## Getting default content for template

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

Returns an array of default content for the template's fields.
Primarily intended for understanding the API/order structure or as default values
for a template preview.

### HTTP Request

`GET http://api.adrapid.com/templates/:id/defaults`


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

