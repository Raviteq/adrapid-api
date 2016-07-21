# Medias

The medias API provides a simple interface to upload medias of any format and get a preview url that is suitable for webpages.
The uploaded medias can also be used on orders, allowing the re-use of medias for different orders.

## Retrieve

Get all the medias uploaded. (TODO: Add query params for search, pagination, etc)

`GET http://api.adrapid.com/medias/`

```json
[{
  "id": "1234",
  "name": "my image",
  "type": "image",
  "preview": "http://medias.adrapid.com/1234/preview",
  "thumbnail": "http://medias.adrapid.com/1234/thumbnail"
},
{
  "id": "5678",
  "name": "my video",
  "type": "video",
  "preview": "http://medias.adrapid.com/5678/preview",
  "thumbnail": "http://medias.adrapid.com/5678/thumbnail"
}]
```

<aside class="success">
Hint: dynamically generate a thumbnail in any size using URL formatted like `http://api.adrapid.com/thumbnail/$WIDTH/path-to-file.jpg. Thumbnails are cached and are generated very quickly. 
</aside>


## Upload

> upload a file

```shell
curl http://api.adrapid.com/medias 
  -F test=@my-image.jpg 
  -H "Authorization: my API key"
```

> upload a file by URL

```shell
curl http://test.adrapid.com/api/medias 
  -H "Authorization: my API key" 
  -F "myfile=http://test.adrapid.com/uploads/client_uploads/demo/img/36b0_Camera1024x1024.png"
```

> upload a base64-encoded image

```shell
curl "http://test.adrapid.com/api/medias"
  -H "Authorization: my API key" 
  -F "myfile=data:image/png;base64,[...]"
```

> example result

```json
{
  "myfile": {
    "id":             1234,
    "original":       "http://medias.adrapid.com/uploads/client/myfile.png",
    "preview":        "http://medias.adrapid.com/uploads/client/myfile_preview.png",
    "thumbnail":      "http://medias.adrapid.com/uploads/client/myfile_thumb.png",
    "original_size":  "1024x1024",
    "preview_size":   "600x600",
    "thumb_size":     "240x240"
  }
}
```

The medias API supports many different media formats. For the complete list please see table XX.
The uploaded medias are transcoded to a format suitable to be previewed in a webpage.
Several methods for sending files are provided. Files can be sent either as regular file upload, as an URL, or as base64-encoded strings. Several images may be uploaded in a single request. 
Use this API to upload files. The returned media ID can be used to track transcoding process
(see the *media progress* API).

`POST http://api.adrapid.com/medias/`

## Crop

```shell
curl test.adrapid.com/api/debug
  -d "image=http://my-site.com/my-image.jpg" 
  -d "x=29.14%" 
  -d "y=18.52%" 
  -d "width=34.32%" 
  -d "height=22.72%"
  -H "Authorization: my API key"
```

Images can be cropped by suppling extra parameters to the *medias* method. The available parameters are listed in the table below. At least one parameter must be provided. 
AdRapid does not enforce aspect ratio. If either width or height is omitted, the image will be cropped according to the original aspect ratio.

The values may be set as pixels or as a percentage.  

Thumbnails may be used, AdRapid will perform the cropping on the original image and return a thumbnail. This ensures maximum image quality, while avoiding sending unnecessarily much data to/from the client. 

Cropping parameters may be supplied when uploading medias to instantly crop the file(s) according to the rules specified. If multiple images are supplied in the same request, the cropping rules will be applied to all images supplied. To crop a previously uploaded image, supply the ID or URL for the image.



### Parameters
Parameters may be defined in pixels or as percentages.

Parameter | Description
--------- | -----------
x | pixels/percentage from the left side
y | pixels/percentage from the left side
width | pixels/percentage of crop width
height | pixels/percentage of crop height



## Progress

The transcoding process can take some time, so in order to track the progress the following API is provided.
The progress is reported as an Integer ranging from 0 to 100.

### SSE Endpoint

`http://api.adrapid.com/medias/:id/`
