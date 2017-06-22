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
{
  "count": 3,
  "rows": [
    {
      "id": "b5147d54-9666-40fa-85f1-90d62c2356df",
      "name": "City",
      "data": {...}
    },
    {
      "id": "02ce42ed-2d5e-49a9-87fc-36b3da6b9e3b",
      "name": "Multicar",
      "data": {...}
    },
    {
      "id": "4cbd59ef-cf43-4c44-9866-f55ac2201a0a",
      "name": "Product",
      "data": {...}
    }
  ]
}
```

Get available templates for a given client. Returns a list of available templates for the client with the supplied `public API key`.

For each template, a `template ID`, `identifier`, `name` and `thumbnail` is supplied. The `template ID` is unique for the template, and must be included in the `order request` for identifying the selected template. 

The `name` and `identifier` fields contain names of the template, which you may use internally as you wish - ie. for identifying templates or displaying readable template names to the end user.

To get the rules for a specific template, call the `template rules` method, supplying the `template ID` to the method call.

### HTTP Request

`GET http://api.adrapid.com/templates`



### Filtering templates

Templates can be filtered to only include templates matching the given search parameters. The number of templates may also be limited, and there is also the option to specify the sorting order.


Parameter | Default | Description
--------- | ------- |-----------
name | | Template name (case-insensitive)
limit | 100 |  Maximum number of templates to return
offset | 0 | Offset from start
order | name | Sorting
formats | | Require the specified format(s)


### Sorting templates
Templates can be sorted by the following columns, in either ascending or descending order.

Parameter | Description
---------- | ----------
name | Template name (default)
createdAt | Creation date
updatedAt | Date last modified
id | Unique UUID


Example:
`GET http://api.adrapid.com/templates?name=City&formats=980x300,300x300&order=updatedAt`


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
TODO: add example content for API v2
```

Get the rules for a given template. The rules of a template defines which datatypes are allowed for every field available in the template (texts, images, colors), as well as the supported output formats.

Images are resized to optimally fit the provided image area when rendering every banner, however, an optimal ratio is supplied in the rules for image fields. Images should preferably be provided in the largest resolution possible, especially when producing ads for printed materials.


The following table shows the available field types:

type | Description
--------- | -----------
text | A string of text of a maximum length
image | An valid image
color | A valid color specification

### HTTP Request

`GET http://api.adrapid.com/templates/:id`


### URL parameters

Parameter | Description
--------- | -----------
:id | The ID of template.


## Get available formats

```shell
curl "http://api.adrapid.com/formats"
  -H "Authorization: my API key"
```

Retreive a list of all available formats for all available templates.

`GET http://api.adrapid.com/formats`


## Retrieving template preview

<aside class="warning">Currently not implemented in API v2</aside>

It is also possible to retrieve a quick preview of a template before actually sending
a time consuming order.

Returns a html preview.


### HTTP Request

`GET http://api.adrapid.com/templates/:id/preview`

### URL parameters

Parameter | Description
--------- | -----------
id | The ID of template.

