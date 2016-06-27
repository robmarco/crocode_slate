---
title: CROCODΞ - API Documentation

language_tabs:
  - shell
  - ruby

toc_footers:
  - <a href='#'>Sign Up for a Developer Key</a>

# includes:
#  - errors

search: true
---

# Introduction

> Libraries for this API are [available in several languages](http://www.github.com/crocode-mobi)

<br>
> Api Endpoint

```shell
https://api.crocode.mobi
```

```ruby
https://api.crocode.mobi
```

This API is organized around [REST](http://en.wikipedia.org/wiki/Representational_State_Transfer). Our API has predictable, resource-oriented URLs, and uses HTTP response codes to indicate API errors. We use built-in HTTP features, like HTTP authentication and HTTP verbs, which are understood by off-the-shelf HTTP clients.

We support [cross-origin resource sharing](http://en.wikipedia.org/wiki/Cross-origin_resource_sharing), allowing you to interact securely with our API from a client-side web application (though you should never expose your secret API key in any public website's client-side code).

[JSON](http://www.json.org) is returned by all API responses, including errors, although our API libraries convert responses to appropriate language-specific objects.


# Authentication

```shell
# Authentication using HTTP basic auth.
curl 'https://api.crocode.mobi/v1/login' \
  -u {key}:

# Alternatively pass a Bearer token in an Authorization header.
curl 'https://api.crocode.mobi/v1/login' \
  -H 'Authorization: Token token={key}'
```

```ruby
require 'crocode-client'

api = Crocode::APIClient.authorize!('key')
```
> Make sure to replace `key` with your API key.


Authenticate your account when using the API by including your secret API key in the request. You can manage your API keys in the [Dashboard](http://www.croode.mobi/developers). Your API keys carry many privileges, so be sure to keep them secret! Do not share your secret API keys in publicly accessible areas such GitHub, client-side code, and so forth.

Authentication to the API is performed via [HTTP Basic Auth](https://en.wikipedia.org/wiki/Basic_access_authentication). Provide your API key as the basic auth username value. You do not need to provide a password.

If you need to authenticate via bearer auth (e.g., for a cross-origin request), use

<code>-H "Authorization: Token token=sk_test_BQokikJOvBiI2HlWgH4olfQ2"</code>

instead of

<code>-u sk_test_BQokikJOvBiI2HlWgH4olfQ2:.</code>

# Errors

This API uses conventional HTTP response codes to indicate the success or failure of an API request. In general, codes in the <code>2xx</code> range indicate success, codes in the <code>4xx</code> range indicate an error that failed given the information provided (e.g., a required parameter was omitted, an operation failed, etc.), and codes in the <code>5xx</code> range indicate an error with API servers (these are rare).

Not all errors map cleanly onto HTTP response codes, however. When a request is valid but does not complete successfully (e.g., an operation is declined), we return a <code>402</code> error code.

## HTTP Status codes

Code | Title | Description
---- | ----- | -----------
200 |	OK | The request was successful.
201	| Created	| The resource was successfully created.
202	| Async created	| The resource was asynchronously created
400	| Bad request	| Bad request.
401 | Unauthorized | Not valid API Key provided.
404	| Not found |	The resource does not exist.
422	| Validation error |	A validation error occurred.
50X	| Internal | Server Error	An error occurred with our API.

## Error types

> Example error response.

```json
{
  "error": {
    "type": "params_invalid",
    "message": "Name is required"
  }
}
```

All errors are returned in the form of JSON with a type and optional message.

Type | Description
---- | -----------
params_invalid | Your parameters were not valid.
unknown_record | Record was not found.
unknown_route | URL was not valid.
queued | Lookup queued. Try this request again in a few minutes.
rate_limit | The request has been rate limited.
api_error | Internal API error.

# Webhooks

Certain requests may have an asynchronous response (since there’s some complex background processing involved). For these requests you can either poll the endpoint, or give us a webhook URL you want to be called when the request has finished processing.

You can set a webhook URL endpoint in your [Dashboard](http://www.crocode.mobi/developers) to be used with all requests.

To link up your requests to webhooks you can pass a webhook_id parameter when making these calls, containing a custom defined webhook identifier. We’ll pass this identifier back to you with the webhook request.

If you return anything other than a HTTP <code>200</code> status to the webhook POST then we’ll try to deliver the webhook up to 5 times with an exponential backoff.

# Service 1

## Get Resource

This endpoint retrieves a specific resource.

```ruby
require 'crocode-client'

api = Crocode::APIClient.authorize!('key')
api.resource.get(id)
```

```shell
curl "http://api.crocode.mobi/v1/resources/id"
  -H "Authorization: Token token=key"
```

> The above command returns JSON structured like this:

```json
{
  "resource": {
    "id": 1,
    "name": "Fluffums",
    "breed": "calico",
    "fluffiness": 6,
    "cuteness": 7
  }
}
```

### HTTP Request

`GET http://api.crocode.mobi.com/v1/resources<ID>`

### URL Parameters

Parameter | Description
--------- | -----------
ID | The ID of the kitten to retrieve

<div class="wrap">
  <div class="alert notice">Inside HTML code blocks like this one, you can't use Markdown, so use <code>&lt;code&gt;</code> blocks to denote code.</div>
</div>

Lorem ipsum dolor sit amet, consectetur adipiscing elit. In erat mauris, faucibus quis pharetra sit amet, pretium ac libero. Etiam vehicula eleifend bibendum. Morbi gravida metus ut sapien condimentum sodales mollis augue sodales. Vestibulum quis quam at sem placerat aliquet. Curabitur a felis at sapien ullamcorper fermentum. Mauris molestie arcu et lectus iaculis sit amet eleifend eros posuere. Fusce nec porta orci.

Lorem ipsum dolor sit amet, consectetur adipiscing elit. In erat mauris, faucibus quis pharetra sit amet, pretium ac libero. Etiam vehicula eleifend bibendum. Morbi gravida metus ut sapien condimentum sodales mollis augue sodales. Vestibulum quis quam at sem placerat aliquet. Curabitur a felis at sapien ullamcorper fermentum. Mauris molestie arcu et lectus iaculis sit amet eleifend eros posuere. Fusce nec porta orci.

Lorem ipsum dolor sit amet, consectetur adipiscing elit. In erat mauris, faucibus quis pharetra sit amet, pretium ac libero. Etiam vehicula eleifend bibendum. Morbi gravida metus ut sapien condimentum sodales mollis augue sodales. Vestibulum quis quam at sem placerat aliquet. Curabitur a felis at sapien ullamcorper fermentum. Mauris molestie arcu et lectus iaculis sit amet eleifend eros posuere. Fusce nec porta orci.
