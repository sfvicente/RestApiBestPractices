# Rate Limiting


## General

...


## Headers
<br>


### Use the `X-RateLimit-Limit` header to communicate the maximum number of requests permitted for an API endpoint

// TODO: add description.

```http
// TODO: add example
```

<br><br>


### Use the `X-RateLimit-Remaining` header to communicate the number of requests remaining in the current rate limit window

// TODO: add description.

```http
// TODO: add example
```

<br><br>


### Use the `X-Rate-Limit-Reset` header to communicate the remaining window before the rate limit resets

// TODO: add description.

```http
// TODO: add example
```

<br><br>


## Status Codes
<br>


### Always return an HTTP `429 Too Many Requests` response when a rate limit is reached.

A service must return a limiting signal when the defined limits are reached.

// TODO: complement description.

```http
// TODO: add example
```

<br><br>