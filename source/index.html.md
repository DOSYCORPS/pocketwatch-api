---
title: Pocketwatch API Reference

language_tabs: # must be one of https://git.io/vQNgJ
  - javascript

toc_footers:
  - <a 
      style=color:lime 
      target=_new 
      href=https://api.pocketwatch.xyz/?where_do_you_come_from=docs>API Keys, Monthly Plans</a>
  - <a href=https://github.com/dosyago-corp/pocketwatch.js>Client library on GitHub</a>
  - <a href=https://github.com/dosyago-corp/service-issues/issues>Open an Issue</a>
  - <a href='https://github.com/lord/slate'>Super Doc Powers &#x26a1; by Slate</a>

includes:
  - errors

search: true
---

# Introduction

  Welcome to the Pocketwatch API Reference. 

  You can use our API to access Pocketwatch API endpoints, which let you control timers, API keys and subscriptions in our system.

  We have language bindings in JavaScript! You can view code examples in the dark area to the right.

# Authentication

  > To authorize, use this code:

  ```javascript
  const pocketwatch = require('@dosy/pocketwatch');

  let api = pocketwatch.authorize('<your API key>');
  ```

  > Make sure to replace `<your API key>` with your API key.

  Pocketwatch uses API keys to allow access to the API. You can register a new Pocketwatch API key at our [developer portal](https://api.pocketwatch.xyz/).

  Pocketwatch expects your `apiKey` be included in all API requests to the server in as a parameter of the POST body in either `application/json` 

  `"apiKey": "<your api key>"`

  or in `application/x-www-form-urlencoded`

  `apiKey=<your api key>`

  <aside class="notice">
    You must replace <code>&lt;your API key&gt;</code> with your personal API key.
  </aside>

# Timers

## Create a new Timer

> To create a timer, use this code:

  ```javascript
  const pocketwatch = require('@dosy/pocketwatch');

  let api = pocketwatch.authorize('<your API key>');
  let timers = api.timer.create({
    name: "My new timer",
    interval: "second",
    intervalCount: 1,
    duration: "week",
    durationCount: 2
  });
  ```

> The above command returns JSON structured like this:

  ```javascript
  {
    "action": "create",
    "status": "success",
    "timer": {
      "keyName": "<timer keyName>"
    }
  }
  ```

  This endpoint creates a new timer. It will begin running immediately.

### HTTP Request

  `POST https://api.pocketwatch.xyz/v1/timer/new`

### Body Parameters

  Parameter | Description
  --------- | -----------
  interval |  The unit to count interval time in. Must be one of "second", "minute", "hour", "day", "week", "month"
  intervalCount | The number of unit times between intervals for your timer. Must be positive whole number greater than or equal to 1
  duration | The unit to count total timer duration in. Must be one of "second", "minute", "hour", "day", "week", "month"
  durationCount | The number of duration units your timer will exist for. Must be positive whole number greater than or equal to 1
  url |  The full URL that your timer will request ( only http or https schemes are supported )
  method | The HTTP method your timer will use to request your URL. Must be one of GET or POST.
  name | A descriptive name for your timer. Is not required to be unique. Can contain spaces. Optional.

  <aside class="success">
    Remember — Include `apiKey` with the above request to authenticate!
  </aside>

## Delete a Specific Timer

> To delete one of your timers, use code like this:

  ```javascript
  const pocketwatch = require('@dosy/pocketwatch');

  let api = pocketwatch.authorize('<your API key>');
  const result = api.timer.delete('<timer keyName>');
  ```

> The above command returns JSON structured like this:

  ```javascript
  {
    "action": "delete",
    "keyName": "<timer keyName>",
    "status": "success"
  }
  ```

  This endpoint deletes a specific timer.

  <aside class="warning">
    Once you delete a timer you cannot get it back and its execution will stop immediately. 
  </aside>

### HTTP Request

  `POST https://api.pocketwatch.xyz/v1/delete/timer`

### Body Parameters

  Parameter | Description
  --------- | -----------
  keyName | The keyName of the timer to delete

  <aside class="success">
    Your plan's hit quota be credited for the approximate amount of hits remaining on the deleted timer.
  </aside>

# API Keys

## Refresh an API Key

> To refresh your current API key, and be issued a new API key, do this:

  ```javascript
  const pocketwatch = require('@dosy/pocketwatch');

  let api = pocketwatch.authorize('<your API key>');
  const result = await api.key.refresh();
  ```

> The above command returns JSON structured like this:

  ```javascript
  {
    "action": "refresh",
    "status": "success",
    "oldKey": "<your old API key>",
    "apiKey": "<your new API key>"
  }
  ```

  This endpoint refreshes your API key. 

### HTTP Request

  `POST https://api.pocketwatch.xyz/v1/key/refresh`

  <aside class="notice">
    The `oldKey` will become invalid. This nearly always happens immediately, but
    occasionally it may not be immediate. Plan to begin using your new `apiKey` for all
    subsequent requests.
    Remember — Include `apiKey` with the above request to authenticate!
  </aside>

# Subscriptions

## Cancel a subscription

> To cancel your subscription, issue this command:

  ```javascript
  const pocketwatch = require('@dosy/pocketwatch');

  let api = pocketwatch.authorize('<your API key>');
  const result = await api.subscription.cancel();
  ```

> The above command returns JSON structured like this:

  ```javascript
  {
    "action": "cancel",
    "status": "success",
    "endsAt": "<timestamp at which the subscription will end>"
  }
  ```

  This endpoint cancels your subscription. 

### HTTP Request

  `POST https://api.pocketwatch.xyz/v1/subscription/cancel`

  <aside class="warning">
    Please note &mdash; we do not offer partial refunds if you paid for an entire billing period and then cancel part way through. Instead, the subscription will work until the end of your current billing period, at which time it will cease. 
  </aside>
