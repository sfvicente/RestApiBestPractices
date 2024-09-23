# Rate Limiting
Rate limiting is a technique used to control the number of requests that a client (such as an application or user) can make to an
API within a defined period of time. The purpose of rate limiting is to protect the API from being overwhelmed by too many requests,
which can lead to degraded performance, increased latency, or even denial of service.

## General Guidelines

### Always return an HTTP `429 Too Many Requests` response when a rate limit is reached under normal conditions
A `429 Too Many Requests` response should be returned when clients exceed the defined rate limits, accompanied by headers indicating the
limit, remaining quota, and when to retry.

**Client Request**
```http
GET /api/products
```

**Server Response**
```http
HTTP/1.1 429 Too Many Requests
Content-Type: application/json
Retry-After: 60
X-RateLimit-Limit: 100
X-RateLimit-Remaining: 0
X-RateLimit-Reset: 1627776000

{
  "error": "Too Many Requests",
  "message": "You have exceeded the rate limit. Please wait 60 seconds before retrying."
}
```

The example displays the response returned for a request when the rate limit for an endpoint has been exceeded. This ensures
clients are informed of rate limit violations and can adjust their request behavior.

Tags: `rate limiting` `HTTP status code` `429 Too Many Requests`
<br><br>


## Documentation and Communication Guidelines

### Clearly communicate rate limiting policies to consumers through documentation
The rate limiting policies should be clearly communicated to API consumers through documentation. This transparency helps
consumers understand the limits imposed on their requests, how those limits are calculated, and the appropriate actions
to take when limits are reached. Effective communication of rate limiting policies can prevent misuse, improve user experience,
and maintain the reliability and performance of the API.

 **Documentation Example**:

#### Rate Limiting Policy
Our API employs rate limiting to ensure fair use and maintain optimal performance for all users. Below are the details of our rate limiting policies:

1. **Rate Limit**: 
   - Each user can make up to **100 requests per minute**.

2. **Rate Limit Calculation**:
   - The rate limit is calculated based on the API key or user token associated with each request.

3. **Rate Limit Headers**:
   - We include the following headers in the API response to help you understand your current rate limit status:
     - `X-RateLimit-Limit`: The maximum number of requests allowed in the current time window.
     - `X-RateLimit-Remaining`: The number of requests remaining in the current time window.
     - `X-RateLimit-Reset`: The time at which the rate limit will reset, in UTC epoch seconds.

4. **Exceeded Rate Limit**:
   - If you exceed the rate limit, you will receive a `429 Too Many Requests` response with a `Retry-After` header indicating when you can retry your request.

5. **Best Practices**:
   - Implement exponential backoff and retries in your client application to handle rate limit responses gracefully.
   - Monitor the rate limit headers to adjust your request rate dynamically and avoid hitting the limits.

**Example Response When Rate Limit Is Exceeded**:

#### Client Request
```http
GET /api/products
```
#### Server Response
```http
HTTP/1.1 429 Too Many Requests
Content-Type: application/json
Retry-After: 60
X-RateLimit-Limit: 100
X-RateLimit-Remaining: 0
X-RateLimit-Reset: 1627776000

{
  "error": "Too Many Requests",
  "message": "You have exceeded the rate limit. Please wait 60 seconds before retrying."
}
```

When the client attempts to retrieve a list of products after exceeding the limits of the API, the server responds with
a `429 Too Many Requests` status code. The `Retry-After` header indicates that the client should wait 60 seconds before 
making another request. The response also includes `X-RateLimit-Limit`, `X-RateLimit-Remaining`, and `X-RateLimit-Reset`
headers to provide additional information about the rate limit status.

Tags: `rate limiting` `documentation` `request limits` `429 Too Many Requests` `retry strategies` `client communication` `performance` `rate limit headers` `developer experience`
<br><br>


## Implementation Guidelines

### Use a token bucket or sliding window algorithm for rate limiting

TODO

<br><br>


## HTTP Headers Guidelines

### Always use the `X-RateLimit-Limit` header to communicate the maximum number of requests permitted for an endpoint
The `X-RateLimit-Limit` header should be used to communicate to clients the maximum number of requests permitted for a specific
endpoint within a given time period.

**Client Request**
```http
GET /api/products
```

**Server Response**
```http
HTTP/1.1 200 OK
Content-Type: application/json
X-RateLimit-Limit: 100

{
    ...
}
```

Assuming the `/products` endpoint allows a maximum of 100 requests per minute. When a client makes a request to this
endpoint, the server responds with the `X-RateLimit-Limit` header set to `100`. This indicates to the client that they are 
allowed a maximum of 100 requests within the current minute.

The client can use this information to implement rate limiting on their side, ensuring they don't exceed the allowed number of
requests and risk being throttled by the server.

Tags: `rate limiting` `X-RateLimit-Limit` `request limits` `response headers` `client communication` `performance` `developer experience` `rate limit enforcement`
<br><br>


### Consider using the `X-RateLimit-Remaining` header to communicate the number of requests remaining in the current rate limit window
The `X-RateLimit-Remaining` header informs clients of the number of requests they have remaining within the current rate limit
window. It allows clients to monitor their request usage and adjust their behavior to stay within the allowed limits.

**Client Request**
```http
GET /api/products
```

**Server Response**
```http
HTTP/1.1 200 OK
Content-Type: application/json
X-RateLimit-Limit: 100
X-RateLimit-Remaining: 88
```

In this example, the `X-RateLimit-Limit: 100` header communicates that 100 requests is the maximum number of requests allowed within
the rate limit window. The `X-RateLimit-Remaining: 88` header informs that the client has 88 requests remaining within the current
rate limit window before hitting the limit.

Tags: `rate limiting` `X-RateLimit-Remaining`
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

Tags: `rate limiting` `X-Rate-Limit-Reset`
<br><br>


## Reliability and User Experience Guidelines

### Consider limiting resource usage instead of returning an HTTP `429 Too Many Requests` under severe conditions
During periods of excessive requests, particularly when under attack, indiscriminately returning `429 Too Many Requests` for each
request can strain server resources and risk system overload. Instead:

- **Implement Resource Management**: Consider dropping connections, temporarily banning IP addresses, or utilizing other measures
to mitigate the impact of excessive requests
- **Define Clear Strategies**: Provide specific guidelines on when and how to apply these resource management techniques effectively
- **Maintain User Experience**: Ensure that legitimate users receive appropriate responses or alternative endpoints during severe
conditions to maintain a positive user experience.

These strategies enhance the system's scalability and resilience, protecting against potential attacks while maintaining operational stability.

Tags: `rate limiting` `resource usage` `performance` `HTTP status code` `429 Too Many Requests` `security`
<br><br>


### Implement graceful degradation strategies to ensure essential functionality remains available during rate limit enforcement
Rather than cutting off all service access once a rate limit is reached, gracefully reduce non-critical features or data returned while
keeping essential operations available. This ensures clients can still access vital parts of the service, even when restricted by rate limits.

**Approaches:**
- **Prioritize Critical Endpoints**: Allow certain API operations, like login or account management, to remain accessible even after rate limits on less essential endpoints are enforced.
- **Return Reduced Data Sets**: Instead of fully blocking responses, return partial or simplified responses to reduce load while keeping clients informed.
- **Provide Meaningful Error Messages**: Inform clients clearly when rate limits are exceeded and indicate when they can resume full access, along with ways to stay within the limits.

**Example:**

```http
HTTP/1.1 429 Too Many Requests
Content-Type: application/json

{
  "error": "Rate limit exceeded. Essential functions remain available. Please wait 30 seconds before making additional requests."
}
```

**Benefits:**
- **Continuity**: Critical functionality remains accessible, preserving the user experience.
- **Transparency**: Clients are informed of the limitations and can adjust their behavior accordingly.
- **Load Management**: Gradual enforcement of rate limits helps balance server load without abrupt service disruptions.

- Tags: `rate limiting` `graceful degradation` `critical functionality` `load management` `partial responses` `error handling` `user experience` `performance` `client communication`
<br><br>