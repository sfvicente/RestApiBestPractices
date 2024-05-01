# Rate Limiting

Rate limiting is a technique used to control the number of requests that a client (such as an application or user) can make to an
API within a defined period of time. The purpose of rate limiting is to protect the API from being overwhelmed by too many requests,
which can lead to degraded performance, increased latency, or even denial of service.

## General

### Always return an HTTP `429 Too Many Requests` response when a rate limit is reached under normal conditions.

A service must return a limiting signal when the defined limits are reached.

A 429 Too Many Requests response should be returned when clients exceed the defined rate limits, accompanied by headers indicating the
limit, remaining quota, and when to retry.

This ensures clients are informed of rate limit violations and can adjust their request behavior accordingly.

The following example displays the response headers returned for a request when the rate limit for an endpoint has been exceeded:

```http
HTTP/1.1 429 Too Many Requests
Content-Type: application/json
Retry-After: 3600
X-RateLimit-Limit: 100
X-RateLimit-Remaining: 0
```

<br><br>


## Documentation and Communication

### Clearly communicate rate limiting policies to consumers through documentation

TODO


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

```http
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

The `X-RateLimit-Remaining` header informs clients of the number of requests they have remaining within the current rate limit
window. It allows clients to monitor their request usage and adjust their behavior to stay within the allowed limits.

#### Example:

```http
HTTP/1.1 200 OK
Content-Type: application/json
X-RateLimit-Limit: 100
X-RateLimit-Remaining: 88
```

- `X-RateLimit-Limit: 100`: Communicates the maximum number of requests allowed within the rate limit window (100 requests per hour).
- `X-RateLimit-Remaining: 88`: Informs that the client has 88 requests remaining within the current rate limit window before hitting the limit.

<br><br>


### Use the `X-Rate-Limit-Reset` header to communicate the remaining window before the rate limit resets

// TODO: add description.

When the rate limit is achieved and the application/service receives the error, it can check the `X-Rate-Limit-Reset` HTTP header to
know when the rate-limiting will reset.

```http
HTTP/1.1 429 Too Many Requests
Content-Type: application/json
X-Rate-Limit-Limit: 100
X-Rate-Limit-Remaining: 0
X-Rate-Limit-Reset: 3600
```

<br><br>






### Consider limiting resource usage instead of returning an HTTP `429 Too Many Requests` under severe conditions.

During periods of excessive requests, particularly when under attack, indiscriminately returning `429 Too Many Requests` for each
request can strain server resources and risk system overload. Instead:

- **Implement Resource Management**: Consider dropping connections, temporarily banning IP addresses, or utilizing other measures
to mitigate the impact of excessive requests
- **Define Clear Strategies**: Provide specific guidelines on when and how to apply these resource management techniques effectively
- **Maintain User Experience**: Ensure that legitimate users receive appropriate responses or alternative endpoints during severe
conditions to maintain a positive user experience.

By adopting these strategies, you can enhance the system's scalability and resilience, protecting against potential attacks while
maintaining operational stability.

Additional Tags: Security
<br><br>



## TODO

### Implement graceful degradation strategies to ensure essential functionality remains available during rate limit enforcement

TODO