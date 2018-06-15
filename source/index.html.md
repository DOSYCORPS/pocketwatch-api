---
title: API Reference

language_tabs: # must be one of https://git.io/vQNgJ
  - shell
  - ruby
  - python
  - javascript

toc_footers:
  - <a href='#'>Sign Up for a Developer Key</a>
  - <a href='https://github.com/lord/slate'>Documentation Powered by Slate</a>

includes:
  - errors

search: true
---

# Introduction

Welcome to the Pocketwatch API! You can use our API to access Pocketwatch API endpoints, which can get information on various cats, timers, and breeds in our database.

We have language bindings in Shell, Ruby, and Python! You can view code examples in the dark area to the right, and you can switch the programming language of the examples with the tabs in the top right.

This example API documentation page was created with [Slate](https://github.com/lord/slate). Feel free to edit it and use it as a base for your own API's documentation.

# Authentication

> To authorize, use this code:

```ruby
require 'pocketwatch'

api = Pocketwatch::APIClient.authorize!('<your API key>')
```

```python
import pocketwatch

api = pocketwatch.authorize('<your API key>')
```

```shell
# With shell, you can just pass the correct header with each request
curl "api_endpoint_here"
  -H "Authorization: <your API key>"
```

```javascript
const pocketwatch = require('@dosy/pocketwatch');

let api = pocketwatch.authorize('<your API key>');
```

> Make sure to replace `<your API key>` with your API key.

Pocketwatch uses API keys to allow access to the API. You can register a new Pocketwatch API key at our [developer portal](https://api.pocketwatch.xyz/developers).

Pocketwatch expects for the API key to be included in all API requests to the server in a header that looks like the following:

`Authorization: <your API key>`

<aside class="notice">
You must replace <code><your API key></code> with your personal API key.
</aside>

# Timers

## Get All Timers

```ruby
require 'pocketwatch'

api = Pocketwatch::APIClient.authorize!('<your API key>')
api.timers.get
```

```python
import pocketwatch

api = pocketwatch.authorize('<your API key>')
api.timers.get()
```

```shell
curl "https://api.pocketwatch.xyz/api/timers"
  -H "Authorization: <your API key>"
```

```javascript
const pocketwatch = require('@dosy/pocketwatch');

let api = pocketwatch.authorize('<your API key>');
let timers = api.timers.get();
```

> The above command returns JSON structured like this:

```json
[
  {
    "id": 1,
    "name": "Fluffums",
    "breed": "calico",
    "fluffiness": 6,
    "cuteness": 7
  },
  {
    "id": 2,
    "name": "Max",
    "breed": "unknown",
    "fluffiness": 5,
    "cuteness": 10
  }
]
```

This endpoint retrieves all timers.

### HTTP Request

`GET https://api.pocketwatch.xyz/api/timers`

### Query Parameters

Parameter | Default | Description
--------- | ------- | -----------
include_cats | false | If set to true, the result will also include cats.
available | true | If set to false, the result will include timers that have already been adopted.

<aside class="success">
Remember — a happy timer is an authenticated timer!
</aside>

## Get a Specific Timer

```ruby
require 'pocketwatch'

api = Pocketwatch::APIClient.authorize!('<your API key>')
api.timers.get(2)
```

```python
import pocketwatch

api = pocketwatch.authorize('<your API key>')
api.timers.get(2)
```

```shell
curl "https://api.pocketwatch.xyz/api/timers/2"
  -H "Authorization: <your API key>"
```

```javascript
const pocketwatch = require('@dosy/pocketwatch');

let api = pocketwatch.authorize('<your API key>');
let max = api.timers.get(2);
```

> The above command returns JSON structured like this:

```json
{
  "id": 2,
  "name": "Max",
  "breed": "unknown",
  "fluffiness": 5,
  "cuteness": 10
}
```

This endpoint retrieves a specific timer.

<aside class="warning">Inside HTML code blocks like this one, you can't use Markdown, so use <code>&lt;code&gt;</code> blocks to denote code.</aside>

### HTTP Request

`GET https://api.pocketwatch.xyz/timers/<ID>`

### URL Parameters

Parameter | Description
--------- | -----------
ID | The ID of the timer to retrieve

## Delete a Specific Timer

```ruby
require 'pocketwatch'

api = Pocketwatch::APIClient.authorize!('<your API key>')
api.timers.delete(2)
```

```python
import pocketwatch

api = pocketwatch.authorize('<your API key>')
api.timers.delete(2)
```

```shell
curl "https://api.pocketwatch.xyz/api/timers/2"
  -X DELETE
  -H "Authorization: <your API key>"
```

```javascript
const pocketwatch = require('@dosy/pocketwatch');

let api = pocketwatch.authorize('<your API key>');
let max = api.timers.delete(2);
```

> The above command returns JSON structured like this:

```json
{
  "id": 2,
  "deleted" : ":("
}
```

This endpoint deletes a specific timer.

### HTTP Request

`DELETE https://api.pocketwatch.xyz/timers/<ID>`

### URL Parameters

Parameter | Description
--------- | -----------
ID | The ID of the timer to delete

