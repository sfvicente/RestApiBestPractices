# Caching
The **Caching** section provides best practices for managing the storage and retrieval of API responses to improve
performance, reduce latency, and optimise server resources. It includes strategies for setting cache directives,
distinguishing between public and private caches, and maintaining data freshness while ensuring security.

## General

...


## ...


## Define Cache-Control Headers to Manage Caching Behavior
The `Cache-Control` header provides precise control over how resources are cached by clients, proxies, and CDNs, allowing
APIs to optimize performance while ensuring data consistency. By defining `Cache-Control` directives in API responses,
services can balance the trade-offs between reducing server load and ensuring clients access up-to-date information.  

**Key Directives in `Cache-Control`**  
- **`no-store`**: Prevents caching entirely, ensuring clients fetch fresh data on every request.  
- **`no-cache`**: Allows caching but requires validation with the server before using the cached data.  
- **`private`**: Limits caching to the end client, preventing intermediaries from storing the response.  
- **`public`**: Permits caching by any intermediate cache or client.  
- **`max-age`**: Specifies the maximum time (in seconds) that a resource is considered fresh.  
- **`must-revalidate`**: Forces clients to revalidate the resource once it becomes stale.  

**Example: Caching Response with `Cache-Control` Header**  
```http
HTTP/1.1 200 OK  
Cache-Control: public, max-age=3600  
Content-Type: application/json  

{ "id": 1, "name": "example", "status": "active" }  
```  

**Behavior of Common Directives**  
- **Short-Lived Cache**:  
  ```http
  Cache-Control: public, max-age=60  
  ```  
  Ensures freshness for 60 seconds, after which clients must revalidate or fetch new data.  

- **No Caching**:  
  ```http
  Cache-Control: no-store  
  ```  
  Suitable for sensitive data like login responses or payment details.  

- **Validation Required After Expiry**:  
  ```http
  Cache-Control: private, max-age=120, must-revalidate  
  ```  
  Useful for user-specific data that must stay current after a short cache period.  

**Recommendations**  
- Choose directives that align with the resource's nature and usage patterns.  
  - Use `public` and `max-age` for static or infrequently updated resources.  
  - Use `private` and `no-cache` for user-specific or dynamic content.  
- Combine `ETag` or `Last-Modified` with `Cache-Control` for efficient cache validation.  
- Test cache behavior across different clients and intermediaries to ensure correct interpretation.  
- Clearly document caching rules in the API specification, including default and resource-specific behaviors.  

By carefully configuring `Cache-Control` headers, APIs can achieve a balance between performance, bandwidth usage, and
data consistency, delivering a better user experience while reducing server load.  
<br><br>


## Use ETags for Conditional Requests and Cache Validation
ETags (Entity Tags) provide a mechanism for validating the state of a resource and enabling efficient cache
management. By including ETags in responses, APIs allow clients to determine whether a resource has changed
since it was last fetched, reducing unnecessary data transfer and improving performance.  

ETags are particularly useful for conditional requests, where clients can include the ETag value in headers
like `If-None-Match` or `If-Match` to check resource validity before fetching or updating.  

**Example: ETag in a Response**  
```http
HTTP/1.1 200 OK  
ETag: "abc123"  
Content-Type: application/json  

{ "id": 1, "name": "example", "status": "active" }  
```  

**Example: Conditional GET Request**  
```http
GET /resource/1 HTTP/1.1  
If-None-Match: "abc123"  
```  

**Example: Conditional GET Response (Not Modified)**  
```http
HTTP/1.1 304 Not Modified  
ETag: "abc123"  
```  

**Benefits of Using ETags**  
- **Bandwidth Optimization**: Avoids resending unchanged resources, reducing server and client data usage.  
- **Performance Improvement**: Minimises latency by responding with `304 Not Modified` for unchanged resources.  
- **Concurrent Updates**: Detects and prevents overwriting changes made by others, ensuring consistency.  

**Recommendations**  
- Generate strong or weak ETags based on the use case:  
  - **Strong ETags**: Reflect precise resource state changes (e.g., checksum of content).  
  - **Weak ETags**: Consider semantic equivalence and ignore minor differences (e.g., formatting).  
- Ensure ETags are unique and update them whenever the resource changes.  
- Include ETags in responses for resources with caching potential or frequent updates.  
- Validate client operations (e.g., updates or deletions) using conditional headers to detect conflicts.  
- Document ETag usage and examples in API specifications to ensure consistent client implementation.  

By leveraging ETags for conditional requests and cache validation, APIs can enhance efficiency, improve performance, and ensure reliable interactions between clients and services.  
<br><br>


## Always define resource expiry using the `expires` header
Use the `Expires` header to communicate the precise expiration time of cached resources, ensuring that clients
and intermediaries know when to treat cached data as stale. This facilitates efficient caching and prevents serving
outdated content.  

- **Set Expiration Time**: Include the `Expires` header in HTTP responses to define the exact date and time when the resource becomes stale.  
- **Use UTC Format**: The timestamp in the `Expires` header must use the HTTP-date format, which is a specific subset of the RFC 7231 date/time specification (e.g., `Mon, 18 Dec 2024 12:00:00 GMT`).  
- **Coordinate with Cache-Control**: When used alongside `Cache-Control` headers, ensure the directives are consistent and complementary.  

**Examples**  

1. **Correct Usage**  
```http
HTTP/1.1 200 OK  
Content-Type: application/json  
Expires: Mon, 18 Dec 2024 12:00:00 GMT  
```

2. **Complementing Cache-Control**  
```http
HTTP/1.1 200 OK  
Content-Type: application/json  
Cache-Control: public, max-age=3600  
Expires: Mon, 18 Dec 2024 12:00:00 GMT  
```  

**Scenarios**  
- **Static Resources**: For assets like images, scripts, or stylesheets, use `Expires` to define how long they should remain cached.  
- **API Responses**: For dynamic content, combine `Expires` with validation mechanisms (e.g., `ETag`, `Last-Modified`) to allow clients to confirm freshness.  
- **Content Updates**: Adjust `Expires` values to ensure users see updated content promptly when necessary.  

**Benefits**  
- **Improved Performance**: Reduces redundant requests to the server by allowing valid cached responses to be reused.  
- **Clear Communication**: Eliminates ambiguity about cache validity by specifying exact expiration times.  

**Cautions**  
- **Synchronization with Updates**: Ensure `Expires` values reflect the actual validity of the resource to avoid serving outdated data.  
- **Time Skew**: Clients and servers should synchronize clocks to avoid inconsistencies in interpreting expiration times.  

**Tags**: caching, http headers, expires, api response optimization.
<br><br>


## Leverage 304 Not Modified Responses to Save Bandwidth
Efficient use of `304 Not Modified` responses reduces bandwidth usage and improves client performance by avoiding
the retransmission of unchanged resources. Implementing this feature ensures clients receive updated data only
when necessary, optimising resource consumption.

**Examples**  
1. **Conditional GET Request with ETag**  
   **Request**:  
   ```http
   GET /items/123 HTTP/1.1  
   If-None-Match: "abc123"  
   ```  
   **Response** (unchanged resource):  
   ```http
   HTTP/1.1 304 Not Modified  
   ```  

2. **Conditional Request with Last-Modified**  
   **Request**:  
   ```http
   GET /items/123 HTTP/1.1  
   If-Modified-Since: Wed, 20 Dec 2023 12:00:00 GMT  
   ```  
   **Response** (updated resource):  
   ```http
   HTTP/1.1 200 OK  
   Content-Type: application/json  
   ...  
   ```  

**Implementation Guidelines**  
1. Ensure `ETag` or `Last-Modified` headers are included in responses.  
2. Validate incoming conditional headers (`If-None-Match`, `If-Modified-Since`).  
3. Return `304 Not Modified` when appropriate to indicate no resource changes.  

**Benefits**  
- Reduces redundant data transmission.  
- Enhances client performance by leveraging cached resources.  
- Improves overall scalability of API services.  

Proper implementation of `304 Not Modified` responses ensures efficient bandwidth usage and seamless integration for client applications.
<br><br>


## Avoid caching for sensitive data

## Avoid caching for dynamic data
Dynamic data represents frequently changing information that may lose relevance or accuracy quickly if cached. Avoid
caching such data to ensure clients always receive up-to-date responses, maintaining the integrity and timeliness of the API�s output.  

**Examples of Dynamic Data**  
- Real-time stock prices  
- Live sports scores  
- Current user session details  
- Order statuses in progress  

**Risks of Caching Dynamic Data**  
1. **Stale Information**: Cached responses might provide outdated data, leading to incorrect client actions or decisions.  
2. **Inconsistent Behaviour**: Users may observe discrepancies between cached data and the actual state, creating confusion or undermining trust.  
3. **Reduced Reliability**: Time-sensitive applications relying on outdated data may fail to perform as expected.  

**Implementation Guidelines**  
1. **Set Cache-Control Headers**  
   - Use headers such as `Cache-Control: no-cache, no-store, must-revalidate` to prevent caching by clients and intermediaries.  
   - Example:  
     ```http
     Cache-Control: no-cache, no-store, must-revalidate
     Pragma: no-cache
     Expires: 0
     ```  

2. **Mark Responses as Non-Cacheable**  
   - Use HTTP status codes (e.g., 200) with headers explicitly indicating no caching for dynamic endpoints.  

3. **Validate Responses on Each Request**  
   - Ensure servers process each request afresh without relying on prior responses, even when intermediaries attempt to cache.  

4. **Document Dynamic Endpoints**  
   - Clearly specify which endpoints provide dynamic data and should not be cached, ensuring proper client and integrator understanding.  

**Recommendations**  
- Separate dynamic and static endpoints to enable tailored caching strategies.  
- Regularly review API behaviour to identify endpoints with inadvertently cached responses.  
- Monitor and log response freshness to detect and address caching-related issues.  

**Key Benefits of Disabling Caching for Dynamic Data**  
- Ensures real-time accuracy, critical for decision-making applications.  
- Prevents user-facing inconsistencies and enhances trust in the API.  
- Reduces the risk of operational errors stemming from stale data.  

By avoiding caching for dynamic data, APIs can deliver timely, accurate information, ensuring consistency and reliability in applications handling sensitive or real-time workflows.
<br><br>


## Enable Client-Side Caching for Static Resources

## Invalidate Cached Data When Resources Change
Cached data must be invalidated promptly when the underlying resource changes to ensure clients always receive
up-to-date information. Failing to invalidate stale caches can lead to inconsistencies, incorrect data, and a
poor user experience.

- **Leverage Cache Invalidation Headers**: Use headers like `ETag` and `Last-Modified` to inform caches of the resource�s current state and allow efficient validation.  
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
- **Use `private` for Sensitive Data**: Mark responses as `private` to ensure caching only occurs in the user�s browser or local cache, avoiding storage in shared caches.  
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
- **Sensitive Data**: Use `private` or `no-store` for user-specific or confidential data to ensure it�s not cached in shared systems.  
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