# Rate Limiting


## General
Rate limiting is a technique used to control the number of requests that a client (such as an application or user) can make to an
API within a defined period of time. The purpose of rate limiting is to protect the API from being overwhelmed by too many requests,
which can lead to degraded performance, increased latency, or even denial of service.


## HTTP Headers
HTTP headers are the name or value pairs containing additional information that are transferred between clients and servers
with HTTP requests or responses.
<br>


### Use the `X-RateLimit-Limit` header to communicate the maximum number of requests permitted for an API endpoint
The X-RateLimit-Limit header should be used to communicate to clients the maximum number of requests permitted for a specific API
endpoint within a given time period. It helps clients understand their rate limit and adjust their request behavior accordingly to
avoid hitting rate limits and getting throttled.

**Example**:

Suppose we have an API endpoint `/products` that allows a maximum of 100 requests per hour. When a client makes a request to this
endpoint, the API server responds with the `X-RateLimit-Limit` header set to `100`. This indicates to the client that they are 
allowed a maximum of 100 requests within the current hour.

Example Response Headers:
```
HTTP/1.1 200 OK
Content-Type: application/json
X-RateLimit-Limit: 100
```

In this scenario:
- `HTTP/1.1 200 OK` indicates a successful response.
- `Content-Type: application/json` specifies the content type of the response as JSON.
- `X-RateLimit-Limit: 100` informs the client that they can make up to 100 requests to this endpoint per hour.

The client can use this information to implement rate limiting on their side, ensuring they don't exceed the allowed number of
requests and risk being throttled by the API server. This header helps improve API usage transparency and allows clients to better
manage their interactions with the API.

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


## HTTP `429 Too Many Requests` Status Code
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
