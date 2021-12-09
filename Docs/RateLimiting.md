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


### Return an HTTP `429 Too Many Requests` status when a rate limit is reached on the API

// TODO: add description.

```http
// TODO: add example
```

<br><br>