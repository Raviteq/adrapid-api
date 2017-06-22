# Errors

<aside class="notice">
These are generic errors that can be returned by any of the API calls provided in this reference.
For more specific errors check every API call documentation.
</aside>

The AdRapid API uses the following error codes:

Error Code | Meaning
---------- | -------
400 | Bad Request -- The request is invalid or incorrectly formed.
401 | Unauthorized -- The API/Token key is incorrect.
402 | Payment Required -- The current subscription does not cover the request.
403 | Forbidden -- The request was not authorized.
404 | Not Found -- The specified resource could not be found.
429 | Too Many Requests -- Too many requests.
500 | Internal Server Error -- We had a problem with our server. Try again later.
503 | Service Unavailable -- We're temporarially offline for maintanance. Please try again later.
