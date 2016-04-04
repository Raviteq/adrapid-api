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
The base URL for all API request is `http://api.adrapid.com/`. A set of public methods are available as specified in this document.

# Authentication

> To authorize, use this code:

```javascript
var adrapid = require('adrapid')({
  url: 'http://platform.adrapid.com/api/',
  key: 'my API key',
  token: 'my secret token'
});

```

```shell
# With shell, you can just pass the correct header with each request
curl http://platform.adrapid.com/api/
  -H "Authorization: meowmeowmeow"
```

> Make sure to replace `meowmeowmeow` with your API key.

Each client has an private API-key as well as an public API-key. Every template/project
has its own unique API-key. The private client API-key should never be send in itself,
but is used for generating authentication tokens. The public client API-key is used for
authentication by some API methods.

You can register a new AdRapid API key at our [developer portal](http://adrapid.com/developers).

<aside class="notice">
You must replace <code>meowmeowmeow</code> with your personal API key.
</aside>
