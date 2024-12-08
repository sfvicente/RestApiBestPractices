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

## Avoid caching for sensitive data

## Avoid caching for dynamic data

## Enable Client-Side Caching for Static Resources

## Invalidate Cached Data When Resources Change
Cached data must be invalidated promptly when the underlying resource changes to ensure clients always receive
up-to-date information. Failing to invalidate stale caches can lead to inconsistencies, incorrect data, and a
poor user experience.

- **Leverage Cache Invalidation Headers**: Use headers like `ETag` and `Last-Modified` to inform caches of the resource’s current state and allow efficient validation.  
- **Invalidate Proactively**: When updating or deleting resources, send invalidation instructions to caches (e.g., using `Cache-Control: no-cache` or `max-age=0`).  
- **Support Resource Purging**: Implement mechanisms for purging or updating specific cached resources in shared caches (e.g., CDNs) when changes occur.

**Client Request with Cache Validation**

```http
GET /api/products/123
If-None-Match: "e12345"
```

**Server Response When Resource Has Changed**

```http
HTTP/1.1 200 OK
ETag: "e67890"
Content-Type: application/json

{
  "id": 123,
  "name": "Updated Product",
  "price": 49.99
}
```

**Server Response When Resource Has Not Changed**

```http
HTTP/1.1 304 Not Modified
ETag: "e12345"
```

**Scenarios**  
- **Resource Updates**: When a product or user profile is updated, invalidate or update cached data immediately to reflect the change.  
- **Resource Deletions**: Remove the cache entry for a deleted resource to prevent serving stale data.  
- **Dynamic Content**: Use short `max-age` values or validation headers for frequently changing data to minimise stale cache risks.  

Proper cache invalidation ensures consistency and reliability while balancing performance and data accuracy.

**Tags**: cache invalidation, ETag, cache control, data consistency, REST best practices
<br><br>


## Always distinguish between public and private caches using cache directives
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


## Always set `Vary` headers for content negotiation
Use the `Vary` header to indicate which request headers influence the response content during content
negotiation. This ensures that caches and intermediaries correctly store and serve responses tailored
to client preferences.

- **Content Type**: Include `Accept` in the `Vary` header when the response format depends on the client's preferred media type (e.g., JSON or XML).  
- **Language**: Use `Vary: Accept-Language` when providing responses in multiple languages.  
- **Compression**: Specify `Vary: Accept-Encoding` to signal different compressed versions of the response.  

**Example**

**Client Request**

```http
GET /api/products/123
Accept: application/xml
```

**Response**

```http
HTTP/1.1 200 OK
Content-Type: application/xml
Vary: Accept

<product>
  <id>123</id>
  <name>Laptop</name>
  <price>999.99</price>
</product>
```

**Scenarios**  
- Serving JSON or XML responses based on `Accept`.  
- Localising responses using `Accept-Language`.  
- Delivering compressed responses based on `Accept-Encoding`.  

**Cautions**  
- Avoid listing unnecessary headers in `Vary`, as this can reduce caching efficiency.  
- Test responses across varying header values to ensure the correct behaviour.  

**Tags**: caching, content negotiation, vary header, HTTP headers.  
<br><br>


### Always set `Vary` headers for dynamic responses

When generating dynamic responses that depend on headers like `Authorization` or custom headers, use the `Vary` header to ensure caches do not inadvertently serve incorrect content to clients.

**Guideline**  
- **Authentication and Personalisation**: Include `Authorization` in the `Vary` header for APIs serving personalised or role-specific content.  
- **Custom Headers**: Add any custom request headers that influence the response to the `Vary` header.  

**Example**

**Client Request**

```http
GET /api/products/123
Authorization: Bearer <token>
```

**Response**

```http
HTTP/1.1 200 OK
Content-Type: application/json
Vary: Authorization

{
  "id": 123,
  "name": "Laptop",
  "price": 999.99,
  "discount": 100.00
}
```

**Scenarios**  
- Dynamic pricing or discounts based on user roles.  
- User-specific content or access control using `Authorization` headers.  
- Responses varying by custom client-specific headers.  

**Cautions**  
- Overuse of `Vary` for dynamic responses can lead to cache fragmentation.  
- Validate the headers listed in `Vary` to ensure accurate and efficient caching behaviour.  

**Tags**: caching, dynamic responses, vary header, HTTP headers.  
<br><br>


## Cache Busting Techniques for Versioned Resources

## Document Caching Strategies for Each Endpoint
Clearly document the caching strategies applied to each API endpoint to help clients understand how data is
stored, retrieved, and updated. Proper documentation allows developers to optimise client-side caching, reduce
unnecessary network requests, and ensure data freshness.  

- **Define Caching Headers**: Clearly state the caching headers used (`Cache-Control`, `Expires`, `ETag`, etc.) and their intended behaviour.  
- **Indicate Variability**: Highlight if and how caching depends on request parameters (e.g., query strings) or user roles.  
- **Explain Expiry Policies**: Describe when cached data will expire and under what conditions clients should revalidate the cache.  
- **State Exceptions**: Specify endpoints where caching is explicitly disabled and explain the rationale.  

**Example**  

**Caching Enabled**  
```http
GET /api/products
Cache-Control: max-age=3600, public
ETag: "v1-products-12345"
```  
In this case, the products list is cached for 1 hour (3600 seconds) and revalidated with the provided ETag.  

**Caching Disabled**  
```http
GET /api/orders
Cache-Control: no-store
```  
Here, order data is considered sensitive and is not cached by either public or private caches.  

**Scenarios**  
- **Public Resources**: Document how long resources like product catalogs or static data can be cached.  
- **User-Specific Data**: Highlight caching differences for data unique to authenticated users (e.g., user profiles).  
- **Dynamic Content**: Explain how frequently-changing data should be handled with appropriate caching policies.  

**Cautions**  
- **Undocumented Strategies**: Lack of documentation can lead to inefficient client implementations, stale data, or redundant API calls.  
- **Inconsistent Practices**: Ensure all endpoints follow the documented caching strategies to avoid unexpected behaviour.  

**Tags**: caching, documentation, cache-control, ETag, expires.  