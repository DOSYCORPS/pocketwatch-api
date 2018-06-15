# Errors

<aside class="notice">
  Here's a helpful guide to let you know what's up if you see any of these HTTP errors.
</aside>

The Pocketwatch API uses the following error codes:


Error Code | Meaning
---------- | -------
400 | Bad Request -- Your request is invalid.
401 | Unauthorized -- Your API key is wrong.
404 | Not Found -- The specified endpoint could not be found.
405 | Method Not Allowed -- You tried to access an endpoint with an invalid method.
429 | Too Many Requests -- You're sending requesting too many requests!
500 | Internal Server Error -- We had a problem with our server. Please wait a little bit.
503 | Service Unavailable -- We're feeling really embarrassed. Please tell us how we're doing on our [issues page](https://github.com/dosyago-corp/service-issues/issues)
