# Rate Limiting


## General

...


## HTTP Headers
HTTP headers are the name or value pairs containing additional information that are transferred between clients and servers
with HTTP requests or responses.
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

When the rate limit is achieved and the application/service receives the error, it can check the `X-Rate-Limit-Reset` HTTP header to
know when the rate-limiting will reset.

```http
// TODO: add example
```

<br><br>


## `HTTP 429` Status Code
The HTTP `429 Too Many Requests` response status code indicates that a client has sent too many requests within a defined amount of time.
<br>


### Always return an HTTP `429 Too Many Requests` response when a rate limit is reached under normal conditions.

A service must return a limiting signal when the defined limits are reached.

// TODO: complement description.

The following example displays the response headers returned for a request when the rate limit for an endpoint has been exceeded:

```http
HTTP/1.1 429
X-Rate-Limit-Limit: 1024
X-Rate-Limit-Remaining: 0
X-Rate-Limit-Reset: 1639452294
```

<br><br>


### Consider limiting resource usage instead of returning an HTTP `429 Too Many Requests` under severe conditions.

When handling an excessive volume of requests from a single source, such as when a server is under attack, serving every request
might to be the correct strategy. If a server is forced to respond to each request with an an HTTP `429 Too Many Requests`, it
could drain available resources and risk overloading the system.

Instead, consider limiting resource usage by dropping connections, temporarily banning IP addresses or other measures.

Additional Tags: Security
<br><br>
