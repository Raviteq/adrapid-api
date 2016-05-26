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

```shell
curl -F test=@my-image.jpg http://api.adrapid.com/medias
```

The medias API supports many different media formats. For the complete list please see table XX.
The uploaded medias are transcoded to a format suitable to be previewed in a webpage.
Use this API to upload files. The returned media ID can be used to track transcoding process
(see the *media progress* api).

`POST http://api.adrapid.com/medias/`

## Progress

The transcoding process can take some time, so in order to track the progress the following API is provided.
The progress is reported as an Integer ranging from 0 to 100.

### SSE Endpoint

`http://api.adrapid.com/medias/:id/`
