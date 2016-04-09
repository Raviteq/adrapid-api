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
  - errors

search: true
---

# Introduction 

This is the [AdRapid](http://www.adrapid.com) public API v1.0 documentation

### API URL
The base URL for all API requests is `http://api.adrapid.com/`. A set of public methods are available as specified in this document.

# Authentication

> To authorize, use this code:

```javascript
var adrapid = require('adrapid')({
  url: 'http://api.adrapid.com/',
  key: 'myAPIKey',
  token: 'mySecretToken'
});

```

```shell
# With shell, you can just pass the correct header with each request
curl http://api.adrapid.com/
  -H "Authorization: myAPIKey"
```

> Make sure to replace `myAPIKey` and `mySecretToken` with your API key and token respectively.

Each client has an private API-key as well as an public API-key. Every template/project has an unique API-key/identifier. The private client API-key should never be send in itself, but is used for generating authentication tokens. Currently only the public client API-key is needed for authentication for most of the API methods.

You can register for a new AdRapid API key at our [developer portal](http://adrapid.com/developers).

<aside class="warning">Autentication is disabled for the `adrapiddemo` account. Only the `public key` needs to be provided in all API requests.</aside>

<aside class="notice">
You must replace <code>myAPIKey</code> and <code>mySecretToken</code> with your
personal API key and token respectively.
</aside>

