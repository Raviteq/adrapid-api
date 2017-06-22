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

This is the [AdRapid](http://www.adrapid.com) public API v2.0 documentation

### API URL
The URL endpoint for all API requests is `https://api.adrapid.com/`. A set of public
methods are available as described in this document.


### Description of order workflow
`AdRapid` is an ad creation platform used for producing *html5 banners* as well as ads for print. The platform uses the concept of `users`, `templates` and `banners`. Each user has access to a given set of templates. A template describes the overall layout and animations of an ad. A template contains a set of available `ad formats`, for different types of ads. The user can supply own texts, images and colors, as well as the desired ad formats, thereby creating an `order`. The resulting order is sent to AdRapid and the resulting `banners` are produced and returned to the user.


# Authentication

**TODO:** add description for API tokens, available through account->API keys
Authentication is handled though [JSON web tokens](https://jwt.io/).

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

<aside class="notice">
You must replace <code>my API Key</code> and <code>my secret token</code> with your
personal API key and token respectively.
</aside>
