---
title: API Reference

language_tabs: # must be one of https://git.io/vQNgJ
  - javascript

toc_footers:
  - <a 
      style=color:lime 
      target=_new 
      href=https://api.pocketwatch.xyz/?where_do_you_come_from=docs>API Keys, Monthly Plans</a>
  - <a href='https://github.com/lord/slate'>Super Doc Powers &#x26a1; by Slate</a>

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

```javascript
const pocketwatch = require('@dosy/pocketwatch');

let api = pocketwatch.authorize('<your API key>');
```

> Make sure to replace `<your API key>` with your API key.

Pocketwatch uses API keys to allow access to the API. You can register a new Pocketwatch API key at our [developer portal](https://api.pocketwatch.xyz/).

Pocketwatch expects for the API key to be included in all API requests to the server in as part of the POST body JSON that looks like the following:

```json
{
  ... request ...
  apiKey: "<your API key>"
  ... request ...
}
```

<aside class="notice">
  You must replace <code><your API key></code> with your personal API key.
</aside>

# Timers

## Create a new Timer

```javascript
const pocketwatch = require('@dosy/pocketwatch');

let api = pocketwatch.authorize('<your API key>');
let timers = api.timer.create({
  name: "My new timer",
  interval: { 
    unit: "second",
    count: 1
  },
  duration: {
    unit: "week",
    count: 2
  }
});
```

> The above command returns JSON structured like this:

```json
{
  "action": "create",
  "status": "success",
  "timer": {
    "keyName": "<timer keyName>"
  }
}
```

This endpoint creates a new timer.

### HTTP Request

`POST https://api.pocketwatch.xyz/v1/timer/new`

### Body Parameters

Parameter | Default | Description
--------- | ------- | -----------
name | "", optional | A descriptive name for your timer. Is not required to be unique. Can contain spaces.
url | no default, required | The full URL that your timer will request ( only http or https schemes are supported )
method | GET | The HTTP method your timer will use to request your URL. Must be one of GET or POST.
unit | no default, required | The unit to count interval time in. Must be one of "second", "minute", "hour", "day", "week", "month"
count | no default, required | The number of unit times between intervals for your timer. Must be positive whole number greater than or equal to 1
duration_unit | no default, required | The unit to count total timer duration in. Must be one of "second", "minute", "hour", "day", "week", "month"
duration_count | no default, required | The number of duration units your timer will exist for. Must be positive whole number greater than or equal to 1


<aside class="success">
  Remember — Include apiKey with the above request to authenticate!
<</aside>

## Delete a Specific Timer

```javascript
const pocketwatch = require('@dosy/pocketwatch');

let api = pocketwatch.authorize('<your API key>');
const result = api.timer.delete('<timer keyName>');
```

> The above command returns JSON structured like this:

```json
{
  "action": "delete",
  "keyName": "<timer keyName>",
  "status": "success"
}
```

This endpoint deletes a specific timer.

<aside class="warning">
  Once you delete a timer you cannot get it back and its execution will stop immediately. 
  You will be recredited for the approximate amount of hits remaining on your timer, so those amount of hits will be added back to your quota for your plan.
</aside>

### HTTP Request

`POST https://api.pocketwatch.xyz/v1/delete/timer`

### Body Parameters

Parameter | Description
--------- | -----------
keyName | The keyName of the timer to delete

## Delete a Specific Timer


