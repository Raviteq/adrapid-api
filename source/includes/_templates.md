# Templates

Templates are the basic structure from which a banner or other type of
supported output media (also called *item*) can be generated.
You start by getting all the templates available for the current user, then select the
proper one as well as its rules and supported formats and finally you can you can
send orders based on the given template.

## Get templates

```shell
curl "http://api.adrapid.com/templates"
  -H "Authorization: my API key"
```

```javascript
var adrapid = require('adrapid')({
  url: 'http://api.adrapid.com/',
  key: 'my API key',
  token: 'my secret token'
});

adrapid.templates().then(function(templates){
  // do something with our templates
  console.log(templates);
}, function(err){
  console.error('Error getting templates', err);
});

```

> Example result of calling the get templates method

```json
[{
  "id":         "qual3097a002fdaeeb02a79e877bb9bda7e502ae",
  "name":       "AdRapid product 1",
  "identifier": "adrapid-product00001",
  "thumbnail":  "http://adrapid.com/thumbnail.jpg",
  "group":      "product"
},
{
  "id":         "snowwq97a0l2fdabeb02a79e877bb9bda7e502ae",
  "name":       "Product snow",
  "identifier": "mxm-product_snow",
  "thumbnail":  "http://adrapid.com/thumbnail.jpg",
  "group":      "product"
},
{
  "id":         "service-image_xbeb02a79e877bb9bda7e502ae",
  "name":       "Service image",
  "identifier": "mxm-service_image",
  "thumbnail":  "http://adrapid.com/thumbnail.jpg",
  "group":      "real_estate"
}]
```

Get available templates for a given client. Returns a list of available templates for the client with the supplied `public API key`.

For each template, a `template ID`, `identifier`, `name` and `thumbnail` is supplied. The `template ID` is unique for the template, and must be included in the `order request` for identifying the selected template. 

The `name` and `identifier` fields contain names of the template, which you may use internally as you wish - ie. for identifying templates or displaying readable template names to the end user.

The `thumbnail` field contains a URL to a jpeg image which may be used for displaying a overview of the template in your UI.

The `group` property describes the `content-type` required for the template. Our templates are designed for different use cases - for example, the fields/content required in a template for real estate ads will differ from the fields required in a template for producing online product ads.

To get the rules for a specific template, call the `template rules` method, supplying the `template ID` to the method call.

<aside class="success">
Hint: use the `group` property to filter templates client-side. 
</aside>

### HTTP Request

`GET http://api.adrapid.com/templates`


## Getting rules for template

```javascript
var adrapid = require('adrapid')({
  url: 'http://api.adrapid.com/',
  key: 'my API key',
  token: 'my secret token'
});

adrapid.rules(templateId).then(function(rules){

}, function(err){
  console.error('Error getting templates', err);
});

```

```shell
curl "http://api.adrapid.com/templates/$TEMPLATE_ID"
  -H "Authorization: my API key"
```

> Example result of calling the get template rules method

```json
{
   "id":    "6066cd7b8712507a5b0d547aa64c370a91ac3f91",
   "name":  "demo-phones",
   "formats": [
      "120x600",
      "160x600",
      "200x200",
      "240x400"
   ],
   "fields":[
      {
         "name":        "text_field1_1",
         "label":       "Product name",
         "type":        "text",
         "max_length":  20,
         "default":     "AdRapid Phone"
      },
      {
         "name":        "text_sign2_1",
         "label":       "Price",
         "type":        "text",
         "max_length":  6,
         "default":     "$399"
      },
      {
         "name":        "img_1",
         "label":       "Product image",
         "type":        "image",
         "default":     "http://adrapid.com/image.png"
      },
      {
         "name":        "img_2",
         "label":       "Product logo",
         "type":        "image",
         "default":     "http://adrapid.com/image.png"
      },
      {
         "name":        "color_background1",
         "label":       "Background color",
         "type":        "color",
         "default":     "#b8594c"
      },
      {
         "name":        "color_texts",
         "label":       "Text color",
         "type":        "color",
         "default":     "#ffffff"
      }
   ]
}
```

Get the rules for a given template. The rules of a template defines which datatypes are allowed for every field available in the template (texts, images, colors), as well as the supported output formats.

Rules for maximum text length (total characters) is supplied for every text field.

Images are resized to optimally fit the provided image area when rendering every banner, however, an optimal ratio is supplied in the rules for image fields. Images should preferably be provided in the largest resolution possible, especially when producing ads for printed materials.


The following table shows the available field types:

type | Description
--------- | -----------
text | A string of text of a maximum length
image | An valid image
color | A valid color specification

### HTTP Request

`GET http://api.adrapid.com/templates/:id/rules`


### URL parameters

Parameter | Description
--------- | -----------
:id | The ID of template.


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
