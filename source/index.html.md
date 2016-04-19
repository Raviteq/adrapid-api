---
title: API Reference

language_tabs:
  - shell
  - javascript

toc_footers:
  - <a href='#'>Sign Up for a Developer Key</a>
  - <a href='https://github.com/tripit/slate'>Documentation Powered by Slate</a>

includes:
  - templates
  - orders
  - events
  - medias
  - errors

search: true
---

# Introduction

This is the [AdRapid](http://www.adrapid.com) public API v1.0 documentation


### Basic description of the order workflow
`AdRapid` is a rendering platform used for rendering a variety of `ads`. It supports
a number of different *ad types* - such as *html5 banners*, *flash banners*, *video*,
as well as *print material*.

The rendering platform is based around a concept of `clients`, `templates` and `orders`.

Every `client` has access to a given set of `templates`. A `template` describes the
overall layout of an ad. A template also contains a set of available `ad formats`,
for different types of ads as listed above. The end user supplies texts, images and
colors, as well as the desired `ad formats`, resulting in an `order`.

The resulting order is sent in an `order request`, using the `send order` method. An
`order request` must include the selected template, as well as the desired content
(texts, colors, images).

Orders may be tracked in real time using *server-sent events*. Alternatively, a request
may also be sent to an URL of choice, if specified in the order request.


### API URL
The base URL for all API requests is `http://api.adrapid.com/`. A set of public
methods are available as specified in this document.

# Authentication

> To authorize, use this code:

```javascript
var adrapid = require('adrapid')({
  url: 'http://api.adrapid.com/',
  key: 'my API Key',
  token: 'my secret token'
});

```

```shell
# With shell, you can just pass the correct header with each request
curl http://api.adrapid.com/
  -H "Authorization: myAPIKey"
```

> Make sure to replace `my API Key` and `my secret token` with your API key and token respectively.

Each client has an private API-key as well as an public API-key. Every template/project has a
unique API-key/identifier. The private client API-key should never be send in itself, but is used
for generating authentication tokens. Currently only the public client API-key is needed for
authentication for most of the API methods.

You can register for a new AdRapid API key at our [developer portal](http://adrapid.com/developers).

<aside class="warning">Autentication is disabled for the `adrapiddemo` account - only the `public key` needs to be provided.</aside>

<aside class="notice">
You must replace <code>my API Key</code> and <code>my secret token</code> with your
personal API key and token respectively.
</aside>

