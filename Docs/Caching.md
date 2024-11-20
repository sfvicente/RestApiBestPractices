# Caching
The **Caching** section provides best practices for managing the storage and retrieval of API responses to improve
performance, reduce latency, and optimise server resources. It includes strategies for setting cache directives,
distinguishing between public and private caches, and maintaining data freshness while ensuring security.

## General

...


## ...


## Define Cache-Control Headers to Manage Caching Behavior

## Use ETags for Conditional Requests and Cache Validation

## Implement Proper Expiry with the Expires Header

## Leverage 304 Not Modified Responses to Save Bandwidth

## Avoid Caching for Sensitive or Dynamic Data

## Enable Client-Side Caching for Static Resources

## Invalidate Cached Data When Resources Change

## Distinguish Between Public and Private Caches Using Cache Directives
Properly distinguishing between public and private caches ensures that cached data is stored and served
appropriately, maintaining both performance and security. Cache directives like `public` and `private`
help control where responses can be cached, preventing sensitive information from being exposed to
unintended users.

- **Use `public` for Shared Caches**: Mark responses as `public` when they can safely be cached by shared caching systems, such as CDNs or proxy servers.  
- **Use `private` for Sensitive Data**: Mark responses as `private` to ensure caching only occurs in the user’s browser or local cache, avoiding storage in shared caches.  
- **Combine with Other Directives**: Use `max-age`, `no-store`, or `no-cache` alongside `public` or `private` to fine-tune caching behaviour.

**Client Request**

```http
GET /api/public-data
```

**Server Response with `public` Cache Directive**

```http
HTTP/1.1 200 OK
Cache-Control: public, max-age=3600
Content-Type: application/json

{
  "id": 123,
  "name": "Public Resource",
  "updated_at": "2024-12-01T10:00:00Z"
}
```

**Client Request**

```http
GET /api/user-profile
Authorization: Bearer <token>
```

**Server Response with `private` Cache Directive**

```http
HTTP/1.1 200 OK
Cache-Control: private, no-store
Content-Type: application/json

{
  "id": 456,
  "name": "John Doe",
  "email": "john.doe@example.com"
}
```

**Scenarios**
- **Public Resources**: Cache publicly accessible information (e.g., product catalogues) to improve load times and reduce server load.  
- **Sensitive Data**: Use `private` or `no-store` for user-specific or confidential data to ensure it’s not cached in shared systems.  
- **Dynamic Content**: Combine `no-cache` with appropriate cache directives to validate the data freshness while maintaining security.  

Proper use of cache directives ensures APIs leverage caching benefits without compromising data integrity or security.

**Tags**: cache control, public caches, private caches, HTTP headers, security
<br><br>


## Set Vary Headers for Content Negotiation and Dynamic Responses

## Cache Busting Techniques for Versioned Resources

## Document Caching Strategies for Each Endpoint