# HTTP Status Codes
HTTP status codes are are used in REST APIs for communicating the result of client requests. They indicate whether a specific HTTP request
has been successfully completed and inform the client about the outcome, such as success, redirection, client errors, or server
errors. Proper use of status codes enhances the clarity and efficiency of client-server interactions, helping developers understand and
handle different scenarios appropriately.

## General Guidelines
<br>


### Prefer the use of standard HTTP status codes to represent the outcome of API requests clearly.
Always use standard HTTP status codes to represent the outcome of API requests, ensuring clarity and consistency. This
practice helps clients understand the result of their requests based on well-established semantics.

**Client Request**
```http
GET /api/products/123
```

**Server Response (Success)**
```http
HTTP/1.1 200 OK
Content-Type: application/json

{
  "product_id": 123,
  "name": "Sample Product",
  "price": 19.99
}
```

**Server Response (Resource Not Found)**
```http
HTTP/1.1 404 Not Found
Content-Type: application/json

{
  "error": "Not Found",
  "message": "The requested product with ID 123 was not found."
}
```

To implement proper use of standard HTTP status codes:
- Map each type of API response to the most appropriate standard HTTP status code.
- Ensure the response body provides additional context and details for errors, helping clients understand and resolve issues.
- Regularly review and update the status codes used in your API to adhere to best practices and evolving standards.

Using standard HTTP status codes ensures that clients can easily interpret the outcome of their requests, leading to a more
intuitive and predictable API interaction.

Tags: `status codes` `HTTP` `API design` `standardization` `best practices`
<br><br>


### Ensure consistency in status codes across the entire API to avoid confusion.
Use consistent HTTP status codes throughout your API to provide a uniform and predictable experience for clients. Consistency
helps avoid confusion and ensures that clients can reliably interpret the results of their requests.

**Client Request**
```http
POST /api/orders
Content-Type: application/json

{
  "product_id": 123,
  "quantity": 2
}
```

**Server Response (Success)**
```http
HTTP/1.1 201 Created
Content-Type: application/json

{
  "order_id": 789,
  "product_id": 123,
  "quantity": 2,
  "status": "confirmed"
}
```

**Server Response (Validation Error)**
```http
HTTP/1.1 400 Bad Request
Content-Type: application/json

{
  "error": "Bad Request",
  "message": "The product_id must be a valid integer."
}
```

To ensure consistency in status codes:
- Define and document a set of standard status codes to be used for common scenarios and errors.
- Implement these standard status codes in a uniform manner across all API endpoints.
- Review and test your API to ensure that status codes are applied consistently.
- Educate your development team on the importance of consistent status code usage and provide guidelines for reference.

Ensuring consistency in status codes across your API helps clients predict and understand the behavior of your API, reducing confusion
and enhancing the overall developer experience.

Tags: `status codes` `consistency` `API design` `standardization` `best practices`
<br><br>


### Implement appropriate redirection status codes to inform clients when a resource has been relocated.

// TODO: add description

```http
// TODO: add example
```

// TODO: complement description

```http
// TODO: add example
```

See also: `redirection`
<br><br>


### Always provide detailed error messages and codes in the response body to help clients understand and resolve issues.

// TODO: add description

```http
// TODO: add example
```

// TODO: complement description

```http
// TODO: add example
```

See Also: `errors` `error handling`
<br><br>


## `2xx` Status Codes Guidelines
The 2xx class of HTTP status codes indicates that the request was successfully received, understood, and accepted.
<br>


### Always return `200 OK` for successful `GET`, `PUT`, or `DELETE` requests that include a response body.

// TODO: add description

```http
// TODO: add example
```

// TODO: complement description

```http
// TODO: add example
```

<br><br>


### Always use `201 Created` for successful `POST` requests when a new resource has been created.
When a POST request results in the creation of a new resource, the server should respond with a `201 Created` status
code. This indicates that the request has been fulfilled and has led to the creation of a new resource. The response
should also include a Location header with the URI of the newly created resource and a representation of the resource
in the response body, if applicable.

**Client Request**
```http
POST /articles
Content-Type: application/json

{
  "title": "New Article",
  "content": "Lorem ipsum dolor sit amet, consectetur adipiscing elit."
}
```

**Server Response**
```http
HTTP/1.1 201 Created
Content-Type: application/json
Location: /articles/123

{
  "id": 123,
  "title": "New Article",
  "content": "Lorem ipsum dolor sit amet, consectetur adipiscing elit.",
  "createdAt": "2024-05-15T12:00:00Z",
  "updatedAt": "2024-05-15T12:00:00Z"
}
```

Using `201 Created` provides clear feedback to the client that the resource was successfully created and where it can be accessed.

Tags: `status codes` `201` `Created` `POST` `resource creation` `HTTP headers` `Location header`
<br><br>


### Consider using `202 Accepted` for asynchronous operations where the request has been accepted but processing is not yet complete.
Use the `202 Accepted` status code for asynchronous operations to indicate that the request has been accepted for processing, but the
processing is not yet complete. This informs the client that their request is valid and will be processed, but there will be a delay
in the final response.

**Client Request**
```http
POST /api/orders
Content-Type: application/json

{
  "product_id": 123,
  "quantity": 2
}
```

**Server Response**
```http
HTTP/1.1 202 Accepted
Content-Type: application/json

{
  "message": "Your order has been accepted and is being processed.",
  "order_id": 789,
  "status_url": "/api/orders/789/status"
}
```

**Scenarios**
- Long-Running Processes: When the server needs time to process the request, such as generating a report or performing data analysis.
- Background Jobs: When the request triggers a background job or task that will be processed asynchronously.
- Batch Operations: When the server processes large batches of data, and immediate completion is not feasible.

To implement proper handling of `202 Accepted`:
- Ensure the client receives a confirmation that their request has been received and will be processed.
- Provide a way for the client to check the status of their request, such as a `status_url` or status endpoint.
- Update the client once the processing is complete, either through polling or callbacks.
- Log the accepted requests and their processing status internally for tracking and debugging purposes.

Using the `202 Accepted` status code appropriately ensures that clients are informed of the acceptance of their request and can track
its progress, providing a better user experience for operations that require asynchronous processing.

Tags: `status codes` `202` `Accepted` `asynchronous operations` `long-running processes`
<br><br>


### Always return `204 No Content` for successful `DELETE` requests or `PUT` requests when no content is returned.
The `204 No Content` status code is used to indicate that a request has been successfully processed, but the 
server does not need to return any content in the response body. This is commonly used for DELETE requests, where
a resource is removed, and for PUT requests when an update to a resource is made but there is no need to return
the updated resource in the response.

**Example Request**
```http
PUT /users/456
Content-Type: application/json

{
  "name": "Jane Doe",
  "email": "jane.doe@example.com"
}
```

**Response**
```http
HTTP/1.1 204 No Content
```

Using `204 No Content` provides a clear and efficient way to acknowledge the success of the request while minimizing
the data sent over the network.

Tags: `status codes` `204` `No Content` `DELETE` `PUT`
<br><br>


### Always return `206 Partial Content` when serving partial GET requests to support range queries for large resources.
Use the `206 Partial Content` status code to indicate that a GET request has been successfully processed and that the server
is returning only a part of the resource as specified by the client's `Range` header. This is particularly useful for large
resources such as files or large datasets, where the client may only need a specific portion of the resource at a time.

**Example Request**
```http
GET /documents/largefile.txt
Range: bytes=1000-1999
```

**Response**
```http
// TODO: add example
```

Supporting range queries and returning `206 Partial Content` can improve performance and efficiency by reducing the amount of
data transferred and allowing clients to request only the necessary portions of a resource.

Tags: `status codes` `206` `Partial Content` `GET` `range queries` `large resources` `performance` `efficiency` `HTTP headers` `Range header`
<br><br>


## `3xx` Status Codes Guidelines
The `3xx` class of HTTP status codes indicates that further action needs to be taken by the client to complete the
request. These codes are typically used for redirection, meaning the requested resource has been moved to a different location.

### Always use `3xx` status codes to clearly indicate redirections.

// TODO: add description

```http
// TODO: add example
```

// TODO: complement description

```http
// TODO: add example
```

See also: `redirection`
<br><br>


### Always return `301 Moved Permanently` when a resource has been permanently relocated to a new URL.
Use the `301 Moved Permanently` status code to indicate that the requested resource has been permanently moved to a
new URL. When a client requests a resource that has been relocated, the server responds with a `301 Moved Permanently`
status code and includes the new URL in the `Location` header. This informs the client that the resource should be
accessed using the new URL in future requests.

**Example Request**
```http
GET /blog/old-post-url
```

**Response**
```http
HTTP/1.1 301 Moved Permanently
Location: http://www.example.com/blog/new-post-url
Content-Type: text/html

<html>
<head><title>301 Moved Permanently</title></head>
<body>
<h1>Moved Permanently</h1>
<p>The document has moved <a href="http://www.example.com/blog/new-post-url">here</a>.</p>
</body>
</html>
```

Using `301 Moved Permanently` helps maintain the integrity and continuity of the resource access, ensuring that clients
and search engines update their records to point to the new URL.

Tags: `status codes` `301` `Moved Permanently` `resource relocation` `HTTP headers` `Location header` `URL redirection` `SEO` `client redirection`
<br><br>


### Always use `302 Found` for temporary redirections when a resource is temporarily available at a different URL.

Use the `302 Found` status code to indicate that the requested resource is temporarily available at a different URL specified
in the `Location` header. This tells the client that the resource is temporarily moved and that future requests should still
use the original URL. The client is expected to make a GET request to the URL provided in the `Location` header to retrieve
the resource.

**Client Request**
```http
GET /api/products/123
```

**Server Response**
```http
HTTP/1.1 302 Found
Location: http://api.example.com/api/products-temp/123
Content-Type: application/json

{
  "message": "The product is temporarily available at a different URL. Please follow the Location header to access it."
}
```

This status code is commonly used for the following scenarios:
* Temporary Maintenance
* Temporary Redirects for A/B Testing
* Load Balancing

Using this status code appropriately, ensures that clients are correctly informed about the temporary availability
of resources at different URLs, improving the user experience and maintaining proper resource access.

Tags: `status codes` `302` `Found` `temporary redirection` `HTTP headers` `Location header` `URL redirection` `temporary maintenance` `A/B testing` `load balancing`
<br><br>


### Consider using `303 See Other` to redirect after a POST request, directing the client to retrieve the resource at a different URL.
Use the `303 See Other` status code is used to indicate that the server has successfully processed a POST request, and the
client should retrieve the resulting resource by making a GET request to the URL specified in the Location header. This
status code is typically used to prevent the client from resubmitting the same POST request if the user refreshes the page
or navigates back to it, thereby promoting idempotency and consistency in resource retrieval.

**Example Request**
```http
POST /api/orders
Content-Type: application/json

{
  "productId": 123,
  "quantity": 2
}
```

**Response**
```http
HTTP/1.1 303 See Other
Location: http://api.example.com/api/orders/456
Content-Type: application/json

{
  "message": "Order created successfully. Retrieve the order details at the provided URL."
}
```

Tags: `status codes` `303` `See Other` `POST requests` `redirection` `HTTP headers` `Location header` `idempotency` `resource retrieval`
<br><br>


### Always implement `307 Temporary Redirect` to preserve the original HTTP method while redirecting to a temporary URL
Use the `307 Temporary Redirect` status code to indicate that the requested resource is temporarily available at a 
different URL, and the client should use the original URL for future requests. Unlike the `302 Found` status
code, `307 Temporary Redirect` ensures that the original HTTP method and request body are preserved during the 
redirection. This is crucial for maintaining the integrity of non-GET requests, such as POST, PUT, DELETE, etc.

**Example Request**
```http
POST /api/v1/resource
Host: example.com
Content-Type: application/json

{
  "data": "example"
}
```

**Example Response**
```http
HTTP/1.1 307 Temporary Redirect
Location: http://example.com/api/temp/resource
Content-Type: application/json

{
  "message": "The resource is temporarily available at a different URL. Please use the original URL for future requests."
}
```

**Scenarios**
- **Maintenance**: When a resource is temporarily moved due to maintenance, and you want to ensure that POST, PUT, or DELETE requests are correctly redirected to the temporary location.
- **Load Balancing**: When redirecting traffic to a temporary server to balance the load without changing the original request method.
- **Temporary Resource Relocation**: When a resource is temporarily relocated and will return to the original URL, ensuring that the original HTTP method is preserved.

**Benefits**
- **Method Preservation**: Ensures that the original HTTP method and request body are maintained, preventing unintended changes to the request type.
- **Clarity for Clients**: Clearly informs clients that the resource is temporarily moved and that future requests should use the original URL.
- **Predictability**: Provides a reliable redirection mechanism that maintains the integrity of the original request method.

**Tags:** `307` `Temporary Redirect` `HTTP method preservation` `status codes` `redirection`
<br><br>


### Always use `308 Permanent Redirect` to preserve the original HTTP method while redirecting to a permanent URL
Use the `308 Permanent Redirect` status code to indicate that the requested resource has been permanently moved to
a new URL, and the client should use this new URL for future requests. Unlike the `301 Moved Permanently` status 
code, `308 Permanent Redirect` ensures that the original HTTP method and request body are preserved during the
redirection. This is crucial for maintaining the integrity of non-GET requests, such as POST, PUT, DELETE, etc.

**Example Request**
```http
POST /api/v1/resource
Host: example.com
Content-Type: application/json

{
  "data": "example"
}
```

**Example Response**
```http
HTTP/1.1 308 Permanent Redirect
Location: http://example.com/api/v2/resource
Content-Type: application/json

{
  "message": "The resource has been permanently moved to a new URL. Please use the new URL for future requests."
}
```

**Scenarios**
- **API Versioning**: When an API endpoint is moved to a new version, and you want to ensure that POST, PUT, or DELETE requests are correctly redirected to the new version.
- **Resource Reorganization**: When resources are reorganized and you want to permanently redirect clients to the new structure while preserving the HTTP method.
- **Permanent URL Changes**: When a resource's URL is permanently changed, and you need to ensure that all types of requests are redirected correctly.

**Benefits**
- **Method Preservation**: Ensures that the original HTTP method and request body are maintained, preventing unintended changes to the request type.
- **Clarity for Clients**: Clearly informs clients that the resource has moved permanently and that future requests should use the new URL.
- **Improved SEO**: Helps search engines update their indexes with the new URL, improving the discoverability of the resource.

**Tags:** `308` `Permanent Redirect` `HTTP method preservation` `status codes` `redirection`
<br><br>


## `4xx` Status Codes Guidelines
The 4xx class of HTTP status codes indicates that the client seems to have made an error. These codes are meant
to inform the client about issues with the request.

### Always use `400 Bad Request` for requests that cannot be processed due to client-side errors.
Use the `400 Bad Request` status code to indicate that the server cannot process the request due to a client-side
error. This could be due to malformed syntax, invalid request message framing, or deceptive request routing. Essentially,
the server is informing the client that the request cannot be understood or processed because the error lies on the 
client's side. This status code helps to ensure that the client is aware of the issue and can correct the request before
attempting again.

**Request**
```http
POST /api/users
Content-Type: application/json

{
  "username": "user123",
  "email": "invalid-email-format"
}
```

**Response**
```http
HTTP/1.1 400 Bad Request
Content-Type: application/json

{
  "error": "Bad Request",
  "message": "The email address provided is not in a valid format. Please provide a valid email address."
}
```

**Scenarios**
- Validation Errors: When the client provides invalid data, such as an incorrect email format, missing required fields, or data types that don't match the expected format.
- Malformed Syntax: When the request syntax is malformed, such as incorrect JSON structure or missing brackets.
- Invalid Parameters: When query parameters or path variables are invalid or do not meet the required criteria.

This code ensures that clients are properly informed about issues with their requests, allowing them to correct the
errors and resubmit valid requests. This helps maintain clear communication between the client and server and improves
the overall reliability of the API.

Tags: `status codes` `400` `Bad Request` `client-side errors` `validation errors` `malformed syntax` `invalid parameters` `error handling`
<br><br>


### Always return `401 Unauthorized` when authentication is required and has failed or not been provided.

// TODO: add description

```http
// TODO: add example
```

// TODO: complement description

```http
// TODO: add example
```

See also: `security` `authentication`
<br><br>


### Always use `403 Forbidden` when the client is authenticated but does not have permission to access the resource
Use the `403 Forbidden` status code to indicate that the server understands the client's request and the client is
authenticated, but the client does not have the necessary permissions to access the requested resource. This informs
the client that their identity is recognized, but they do not have the authorization to perform the requested action.

**Example Request**
```http
GET /api/admin/reports
Host: example.com
Authorization: Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJzdWIiOiIxMjM0NTY3ODkwIiwibmFtZSI6IkpvaG4gRG9lIiwiaWF0IjoxNTE2MjM5MDIyfQ.SflKxwRJSMeKKF2QT4fwpMeJf36POk6yJV_adQssw5c
```

**Example Response**
```http
HTTP/1.1 403 Forbidden
Content-Type: application/json

{
  "error": "Forbidden",
  "message": "You do not have permission to access this resource."
}
```

**Scenarios**
- **Insufficient Permissions**: When an authenticated user attempts to access a resource for which they do not have the necessary permissions, such as an admin-only endpoint.
- **Role-Based Access Control**: When access control policies restrict certain actions based on the user's role, and the user's role does not permit the requested action.
- **Resource-Specific Restrictions**: When specific resources have access restrictions that the authenticated user does not meet, such as attempting to modify another user's data.

**Benefits**
- **Clear Authorization Error**: Clearly indicates to clients that they are authenticated but lack the necessary permissions, differentiating from authentication errors.
- **Improved Security**: Helps enforce security policies by ensuring that users can only access resources they are authorized to.
- **Better Client Understanding**: Provides clients with specific feedback about their permission levels, allowing them to understand access limitations.

**Tags:** `403` `Forbidden` `status codes` `security` `authorization` `error handling` `access control`
<br><br>


### Always return `404 Not Found` when a requested resource cannot be found on the server.
Use the `404 Not Found` when the resource the client is trying to access does not exist or is not available at the specified
URL. It informs the client that the resource could not be found, and there is no indication that it will be available
in the future.

**Client Request**
```http
GET /api/products/999
```

**Server Response**
```http
HTTP/1.1 404 Not Found
Content-Type: application/json

{
  "error": "Not Found",
  "message": "The requested product with ID 999 was not found."
}
```

**Scenarios**
- Non-Existent Resources: When the client requests a resource that does not exist, such as a product ID that is not in the database.
- Incorrect URLs: When the client uses an incorrect URL that does not map to any resource on the server.
- Deleted Resources: When the client requests a resource that has been deleted and is no longer available.

Using `404 Not Found` status code ensures that clients are correctly informed when a resource is not available, allowing
them to handle the error gracefully.

Tags: `status codes` `404` `Not Found` `non-existent resources` `incorrect URLs` `deleted resources` `error handling` `resource availability`
<br><br>


### Always use `405 Method Not Allowed` when the HTTP method used is not supported by the resource.
Use the 405 Method Not Allowed status code when the client attempts to use an HTTP method that is not supported by the
resource at the specified URL. This informs the client that the method they used is recognized but not allowed for the
requested resource.

**Client Request**
```http
DELETE /api/products/123
```

**Server Response**
```http
HTTP/1.1 405 Method Not Allowed
Content-Type: application/json
Allow: GET, POST

{
  "error": "Method Not Allowed",
  "message": "The DELETE method is not allowed for the requested resource."
}
```

**Scenarios**
- Unsupported HTTP Methods: When the client uses an HTTP method that is not supported for the resource, such as trying to DELETE a resource that only supports GET and POST.
- Read-Only Resources: When the client attempts to PUT or POST to a resource that is read-only and only supports GET.
- Restricted Actions: When certain actions (like DELETE or PATCH) are not permitted for specific resources due to business logic or security reasons.

Using the 405 Method Not Allowed status code ensures that clients are correctly informed when they use an unsupported HTTP
method, helping them to understand and correct their request methods appropriately.

Tags: `status codes` `405` `Method Not Allowed` `unsupported HTTP methods` `read-only resources` `restricted actions` `error handling`
<br><br>


### Always return `406 Not Acceptable` status code when a content negotiation requested format is not supported
Use the `406 Not Acceptable` status code to indicate that the server cannot generate a response that is acceptable
according to the Accept headers sent in the request. This informs the client that the requested format or media
type is not supported by the server, and therefore, the server cannot fulfill the request in the requested format.

**Example Request**
```http
GET /api/products
Host: example.com
Accept: application/xml
```

**Example Response**
```http
HTTP/1.1 406 Not Acceptable
Content-Type: application/json

{
  "error": "Not Acceptable",
  "message": "The requested format 'application/xml' is not supported. Please request an acceptable format such as 'application/json'."
}
```

**Scenarios**
- **Unsupported Media Types**: When the client requests a response in a format that the server does not support, such as XML when the server only supports JSON.
- **Content Negotiation**: When multiple media types are specified in the Accept header, and none of them are supported by the server.
- **API Versioning**: When the client requests a specific version of the API that the server does not support in the requested format.

**Benefits**
- **Clear Communication**: Informs clients that their requested format is not supported, allowing them to adjust their Accept headers to a format the server can provide.
- **Improved Client-Server Interaction**: Helps ensure that clients request data in formats that the server can generate, leading to smoother interactions.
- **Error Handling**: Provides a specific error status that clients can handle programmatically to request acceptable formats.

**Tags:** `406` `Not Acceptable` `content negotiation` `status codes` `error handling`
<br><br>


### Always return `409 Conflict` when a request could not be processed due to a conflict with the current state of the resource
Use the `409 Conflict` status code to indicate that the request could not be completed because it conflicts with the current
state of the resource. This informs the client that there is a logical conflict that needs to be resolved before the request
can be successfully processed.

**Example Request**
```http
PUT /api/products/123
Host: example.com
Content-Type: application/json

{
  "id": 123,
  "name": "Updated Product Name",
  "version": 1
}
```

**Example Response**
```http
HTTP/1.1 409 Conflict
Content-Type: application/json

{
  "error": "Conflict",
  "message": "The product with ID 123 could not be updated due to a version conflict. The current version is 2."
}
```

**Scenarios**
- **Resource Version Conflicts**: When updating a resource with an outdated version, causing a version conflict.
- **Duplicate Entries**: When attempting to create a resource that would result in a duplicate entry.
- **Business Logic Conflicts**: When the request violates business rules or constraints, such as booking an already booked appointment slot.

**Benefits**
- **Clear Error Indication**: Informs clients about conflicts with the current state of the resource, allowing them to resolve the issue.
- **Conflict Resolution**: Provides specific information about the nature of the conflict, helping clients understand how to correct their requests.
- **Improved Data Integrity**: Ensures that updates and modifications to resources maintain the integrity and consistency of the data.

**Tags:** `409` `Conflict` `status codes` `error handling` `resource state`
<br><br>


### Always use `410 Gone` for resources that have been permanently removed and will not be available again.
Use the `410 Gone` status code when a resource has been permanently removed from the server and is no longer available. This
informs the client that the resource once existed but has been intentionally removed and will not be restored.

**Client Request**
```http
GET /api/products/456
```

**Server Response**
```http
HTTP/1.1 410 Gone
Content-Type: application/json

{
  "error": "Gone",
  "message": "The requested product with ID 456 has been permanently removed."
}
```

**Scenarios**
- Permanently Removed Resources: When a resource, such as a product or article, has been permanently deleted from the database and will not be reintroduced.
- Obsolete Endpoints: When an API endpoint has been permanently removed and clients should not expect it to be available again.
- Decommissioned Features: When a feature or service has been decommissioned and its resources are no longer accessible.

Using the `410 Gone` status code ensures that clients are correctly informed when a resource has been permanently removed, allowing them
to handle the situation appropriately, such as updating references or notifying users.

Tags: `status codes` `410` `Gone` `permanently removed resources` `obsolete endpoints` `decommissioned features` `resource removal` `error handling`
<br><br>


### Always return `415 Unsupported Media Type` when the content type of the request is not supported by the server.

// TODO: add description

```http
// TODO: add example
```

// TODO: complement description

```http
// TODO: add example
```

<br><br>


### Always use `429 Too Many Requests` to indicate that the user has sent too many requests in a given amount of time.

// TODO: add description

```http
// TODO: add example
```

// TODO: complement description

```http
// TODO: add example
```

See Also: `rate limiting`
<br><br>


## `5xx` Status Codes Guidelines
The 5xx class of HTTP status codes indicates that the server is aware that it has encountered an error or is
otherwise incapable of performing the request.


### Always return `500 Internal Server Error` for unexpected server-side issues that do not fall under other specific 5xx categories.

// TODO: add description

```http
// TODO: add example
```

// TODO: complement description

```http
// TODO: add example
```

<br><br>


### Always use `501 Not Implemented` when the server does not support the functionality required to fulfill the request.
Use the `501 Not Implemented` status code to indicate that the server does not support the functionality required to fulfill
the request. This status code is used when the server recognizes the request method but lacks the ability to fulfill it. It
tells the client that the server does not support the functionality necessary to process the request. This can happen if 
the server is missing the feature or if the feature has not been implemented yet.

**Client Request**
```http
PATCH /api/products/123
Content-Type: application/json

{
  "price": 19.99
}
```

**Server Response**
```http
HTTP/1.1 501 Not Implemented
Content-Type: application/json

{
  "error": "Not Implemented",
  "message": "The PATCH method is not supported for updating products."
}
```

**Use Case Scenarios**
- Unsupported HTTP Methods: When the client uses an HTTP method that the server does not support or has not implemented, such as PATCH, TRACE, or CONNECT.
- Unimplemented Features: When the client requests functionality that has not yet been implemented on the server, even if the request method is recognized.
- Deprecated Functionality: When a feature has been deprecated and removed from the server, and the server no longer supports the required functionality to fulfill the request.

Using `501 Not Implemented` helps to clearly communicate to the client that the requested functionality is not available on 
the server. This ensures that clients are informed when the server lacks the functionality to process their request, allowing
them to adjust their requests accordingly or understand the limitations of the server. This improves the clarity and reliability
of the API by providing clear feedback about unsupported features.

<br><br>


### Always return `502 Bad Gateway` when the server, acting as a gateway or proxy, receives an invalid response from an inbound server.
Use the `502 Bad Gateway` status code when your server, functioning as a gateway or proxy, receives an invalid response from an
upstream server. This informs the client that the intermediary server encountered an error while trying to fulfill the request from
another server.

**Client Request**
```http
GET /api/data
```

**Server Response**
```http
HTTP/1.1 502 Bad Gateway
Content-Type: application/json

{
  "error": "Bad Gateway",
  "message": "The server received an invalid response from the upstream server."
}
```

**Scenarios**
- Upstream Server Errors: When the upstream server is down or experiencing issues and sends an invalid response.
- Network Issues: When network problems between the proxy and the upstream server result in an incomplete or corrupt response.
- Configuration Errors: When misconfigurations in the proxy or upstream server lead to unexpected or malformed responses.

To implement proper handling of `502 Bad Gateway`:
- Ensure that the server detects and correctly identifies invalid responses from upstream servers.
- Provide a clear and generic error message in the response to avoid exposing sensitive internal details.
- Log the details of the invalid upstream response internally for debugging and monitoring purposes.
- Monitor upstream server health and performance to proactively address issues that could lead to `502` errors.

Using the `502 Bad Gateway` status code appropriately ensures that clients are informed when intermediary servers encounter issues with upstream
servers, helping them understand the nature of the problem and manage their requests accordingly.

Tags: `status codes` `502` `Bad Gateway` `proxy` `gateway` `upstream server`
<br><br>


### Always use `503 Service Unavailable` when the server is temporarily unable to handle the request, often due to maintenance or overloading.
Use the `503 Service Unavailable` status code to indicate that the server is temporarily unable to handle the request
due to maintenance, overloading, or other temporary conditions. This informs the client that the server is currently
unavailable and that the request should be retried at a later time. It is typically used when the server needs to 
undergo maintenance or when it is overloaded and cannot process additional requests.

**Client Request**
```http
GET /api/products
```

**Server Response**
```http
HTTP/1.1 503 Service Unavailable
Retry-After: 3600
Content-Type: application/json

{
  "error": "Service Unavailable",
  "message": "The server is currently undergoing maintenance. Please try again later."
}
```

**Use Case Scenarios**
- Server Maintenance: When the server is temporarily unavailable due to scheduled maintenance activities.
- Overloaded Servers: When the server cannot handle additional requests due to high traffic or resource limitations.
- Failover Scenarios: During failover events or when the primary server is temporarily unavailable, and requests are being routed to backup servers.

Using `503 Service Unavailable` helps to communicate to clients that the unavailability is temporary and provides guidance
on when they can retry their requests. It ensures that clients are informed about temporary server unavailability, allowing
them to retry their requests at a suitable time. This improves the reliability of the API by managing client expectations
during periods of maintenance or high load.

<br><br>


### Always return `504 Gateway Timeout` when the server, acting as a gateway or proxy, does not receive a timely response from an upstream server.

// TODO: add description

```http
// TODO: add example
```

// TODO: complement description

```http
// TODO: add example
```

<br><br>


### Always use `505 HTTP Version Not Supported` when the server does not support the HTTP protocol version used in the request
Use the `505 HTTP Version Not Supported` status code to indicate that the server does not support the HTTP protocol version
that was used in the client’s request. This informs the client that the version of HTTP specified in the request is not
supported by the server, and therefore, the server cannot process the request.

**Example Request**
```http
GET /api/products
Host: example.com
HTTP-Version: HTTP/1.0
```

**Example Response**
```http
HTTP/1.1 505 HTTP Version Not Supported
Content-Type: application/json

{
  "error": "HTTP Version Not Supported",
  "message": "The HTTP version used in the request is not supported by this server."
}
```

**Scenarios**
- **Deprecated HTTP Versions**: When the client uses an outdated or deprecated version of HTTP, such as HTTP/1.0, which the server no longer supports.
- **Incompatible HTTP Versions**: When the client uses a newer version of HTTP, such as HTTP/2, which the server is not yet compatible with.
- **Protocol Mismatch**: When there is a protocol mismatch between what the client sends and what the server supports, causing incompatibility.

**Benefits**
- **Clear Protocol Error**: Informs clients about the specific issue related to the HTTP version, allowing them to adjust their requests to a supported version.
- **Improved Compatibility**: Helps ensure that clients use compatible HTTP versions, promoting smoother communication between clients and servers.
- **Protocol Upgrade Guidance**: Provides an opportunity to inform clients about supported HTTP versions, encouraging upgrades to more recent and efficient protocols.

**Tags:** `505` `HTTP Version Not Supported` `status codes` `protocol version` `error handling` `compatibility`
<br><br>


### Always use `511 Network Authentication Required` when the client needs to authenticate to gain network access.
Use the `511 Network Authentication Required` status code when the client must authenticate to gain access to the network. This
informs the client that network access is restricted and they must authenticate before proceeding.

**Client Request**
```http
GET /api/data
```

**Server Response**
```http
HTTP/1.1 511 Network Authentication Required
Content-Type: application/json

{
  "error": "Network Authentication Required",
  "message": "You must authenticate to gain network access."
}
```

**Scenarios**
- Captive Portals: When clients are accessing the internet through a captive portal and must log in or accept terms before proceeding.
- Network Access Control: When network policies require authentication before allowing access to resources or services.
- Subscription Services: When access to network services or resources is restricted to authenticated users, such as subscription-based Wi-Fi hotspots.

Using the `511 Network Authentication Required` status code ensures that clients are correctly informed when network authentication
is required, enabling them to take the necessary steps to gain access.

Tags: `status codes` `511` `Network Authentication Required` `authentication`
<br><br>


