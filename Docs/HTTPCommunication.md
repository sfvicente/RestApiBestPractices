# HTTP Communication
HTTP communication in the context of REST APIs involves using standard HTTP methods, also known as verbs, to perform
operations on resources identified by URLs. Each HTTP verb provides a specific action, making REST APIs intuitive and
enabling clear, predictable interactions between clients and servers.

## General Guidelines

...





## HTTP `GET` Method Guidelines
The HTTP GET method is a request method used to retrieve data from a specified resource on the server. It's one of the
most commonly used HTTP methods and is primarily used for fetching information. When a client sends a GET request to a
server, it typically includes parameters in the URL to specify the resource to retrieve or query parameters to filter the results.
<br>


### Always use `GET` requests to read a single resource or a collection of resources.
The `GET` method is used to retrieve representations of resources. `GET` requests are used to fetch data
about a single resource or a collection of resources, and the server responds with the requested data in the body of the
response. Using `GET` for reading resources ensures that clients can obtain the necessary information without causing any side
effects on the server.

**Example**:

#### Example for Single Resource

```http
GET /articles/123
```

- **Request**: Retrieves the article with ID `123`.

```http
HTTP/1.1 200 OK
Content-Type: application/json

{
  "id": 123,
  "title": "An Interesting Article",
  "content": "Lorem ipsum dolor sit amet, consectetur adipiscing elit.",
  "createdAt": "2024-05-15T12:00:00Z",
  "updatedAt": "2024-05-15T12:00:00Z"
}
```

- **Response**: The server responds with a `200 OK` status code and the body contains the details of the article with ID `123`, including its `id`, `title`, `content`, `createdAt`, and `updatedAt` timestamps.

#### Example for Collection of Resources

```http
GET /articles
```

- **Request**: Retrieves the collection of all articles.

```http
HTTP/1.1 200 OK
Content-Type: application/json

[
  {
    "id": 123,
    "title": "An Interesting Article",
    "content": "Lorem ipsum dolor sit amet, consectetur adipiscing elit.",
    "createdAt": "2024-05-15T12:00:00Z",
    "updatedAt": "2024-05-15T12:00:00Z"
  },
  {
    "id": 124,
    "title": "Another Article",
    "content": "Vestibulum ante ipsum primis in faucibus orci luctus et.",
    "createdAt": "2024-05-16T08:00:00Z",
    "updatedAt": "2024-05-16T08:00:00Z"
  }
]
```

- **Response**: The server responds with a `200 OK` status code and the body contains an array of articles, each with its details such as `id`, `title`, `content`, `createdAt`, and `updatedAt` timestamps.

It is a safe and idempotent HTTP method, meaning it does not alter the state of the resource and repeated requests will produce
the same result.

Tags: `HTTP methods` `GET` `resource retrieval` `REST API design` `idempotent` `safe operations`
<br>


### `GET` requests for individual resources that do not exist should generate a `404`.
When a `GET` request is made for an individual resource that is not found on the server, the API should return
a `404 Not Found` status code. This informs the client that the requested resource does not exist, ensuring clarity
and consistency in API behavior.

**Example**:

```http
GET /articles/123
```

- **Request**: Attempts to retrieve the article with ID `123`.

```http
HTTP/1.1 404 Not Found
Content-Type: application/json

{
  "error": "Resource not found",
  "message": "The requested article with ID '123' does not exist."
}
```

- **Response**: The server responds with a `404 Not Found` status code along with a JSON payload providing details
about the error. This communicates to the client that the requested article could not be found.

<br><br>


### `GET` requests for collection resources should return `200` if the collection is empty.
When clients make `GET` requests to retrieve a collection of resources, the API should return a `200 OK` status code
even if the collection is empty. This indicates that the request was successfully processed, and the response body 
will contain an empty array or object representing the collection.

**Example**:

```http
GET /articles
```

- **Request**: Retrieves the collection of articles.

```http
HTTP/1.1 200 OK
Content-Type: application/json

{
  "articles": []
}
```

- **Response**: The server responds with a `200 OK` status code, indicating that the request was successful. The response
body contains an empty array (`"articles": []`), indicating that there are no articles in the collection.

Returning a `200` status for an empty collection maintains consistency in API responses and allows clients to differentiate
between an empty collection and a resource that does not exist.

Tags: `HTTP methods` `GET` `404 Not Found` `resource retrieval` `collection handling` `error handling` `empty collection` `consistent responses`
<br><br>


### GET requests for collection resources should return `404` if the collection is missing.
When clients make `GET` requests to retrieve a collection of resources and the requested collection does not exist
(i.e., it has not been implemented or configured), the API should return a `404 Not Found` status code. This communicates
to the client that the requested endpoint or resource is not available, distinguishing between an empty collection (which
should return `200 OK` with an empty response) and a missing or undefined collection.

**Example**:

```http
GET /articles
```

- **Request**: Attempts to retrieve the collection of articles.

```http
HTTP/1.1 404 Not Found
Content-Type: application/json

{
  "error": "Resource not found",
  "message": "The requested collection '/articles' does not exist."
}
```

- **Response**: The server responds with a `404 Not Found` status code along with a JSON payload providing details about the error. This informs the client that the requested collection (`/articles`) is not available or has not been implemented.

This ensures consistent and meaningful responses for `GET` requests to collection resources, enhancing the clarity and
reliability of API interactions. This practice helps clients differentiate between different states of resource availability,
improving overall usability and error handling.

Tags: `HTTP methods` `GET` `404 Not Found` `collection retrieval` `resource handling` `error handling` `missing resources` `consistent responses`
<br><br>


### `GET` requests on collection resources should provide adequate filter and pagination mechanisms.

// TODO: add description.

```http
// TODO: add example
```

See also: Filtering, Pagination
<br><br>



## HTTP `POST` Method Guidelines
The HTTP POST method is a request method used to submit data to be processed by a specified resource on the
server. It's commonly used when creating new resources or when submitting data to a server that will trigger
a specific action. Unlike GET requests, which retrieve data, POST requests typically include data in the request
body, allowing for more complex data transmission.
<br>


### Successful `POST` requests should generate a `200` status code if resources have been updated.
When clients make `POST` requests to create or update resources, the API should return a `200 OK` status code if the
request was successful and resulted in the modification or creation of resources. This indicates that the operation
was completed successfully, and the response body may include details about the updated resources.

**Example**:

```http
POST /articles
Content-Type: application/json

{
  "title": "New Article",
  "content": "Lorem ipsum dolor sit amet, consectetur adipiscing elit."
}
```

- **Request**: Creates a new article with the specified title and content.

```http
HTTP/1.1 200 OK
Content-Type: application/json

{
  "id": 123,
  "title": "New Article",
  "content": "Lorem ipsum dolor sit amet, consectetur adipiscing elit.",
  "createdAt": "2024-05-15T12:00:00Z",
  "updatedAt": "2024-05-15T12:00:00Z"
}
```

- **Response**: The server responds with a `200 OK` status code, indicating that the `POST` request was successful and the article was created. The response body contains the details of the newly created article, including its `id`, `title`, `content`, `createdAt`, and `updatedAt` timestamps.

Using `200 OK` for successful `POST` requests aligns with HTTP semantics and communicates the successful modification of
resources to clients. This provides clear and consistent feedback to clients about the outcome of `POST` requests,
enabling them to handle resource creation or update operations effectively. This practice enhances the usability and
reliability of your API design.

Tags: `HTTP methods` `POST` `200 OK` `resource creation` `resource update` `success responses` `resource modification` `API usability` `consistent feedback`
<br><br>


### Successful `POST` requests should generate a `201` status code if resources have been created.
When clients make `POST` requests to create new resources, the API should return a `201 Created` status code upon
successful creation. This status code indicates that the request was successful and that a new resource has been 
created on the server.

**Example**:

```http
POST /articles
Content-Type: application/json

{
  "title": "New Article",
  "content": "Lorem ipsum dolor sit amet, consectetur adipiscing elit."
}
```

- **Request**: Creates a new article with the specified title and content.

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

- **Response**: The server responds with a `201 Created` status code, indicating that the `POST` request was successful
and a new article has been created. The `Location` header provides the URI of the newly created article (`/articles/123`).
The response body includes the details of the newly created article, such as its `id`, `title`, `content`, and timestamps.

Tags: `HTTP methods` `POST` `201 Created` `resource creation` `success responses` `Location header` `new resource` `API usability` `resource management`
<br><br>


### If a `POST` request creates a new resource, consider including the URI of the resource in the `Location` header of the response.
When a `POST` request successfully creates a new resource, it is a best practice to include the URI of the newly created
resource in the `Location` header of the response. This provides clients with a direct link to the new resource, allowing
them to easily access, retrieve, or interact with it. 

**Example**:

```http
POST /articles
Content-Type: application/json

{
  "title": "New Article",
  "content": "Lorem ipsum dolor sit amet, consectetur adipiscing elit."
}
```

- **Request**: Creates a new article with the specified title and content.

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

- **Response**: The server responds with a `201 Created` status code, indicating that the `POST` request was successful
and a new article has been created. The `Location` header provides the URI of the newly created article (`/articles/123`).
The response body includes the details of the newly created article, such as its `id`, `title`, `content`, and timestamps.

Including the `Location` header improves the usability of the API by giving clients immediate knowledge of the new resource's
URI, which can be useful for subsequent operations such as `GET`, `PUT`, `PATCH`, or `DELETE` requests on that resource.

Tags: `HTTP methods` `POST` `Location header` `resource creation` `201 Created` `URI` `API usability` `best practices` `new resource`
<br><br>


### If a `POST` request creates a new resource, the response body should contain a representation of the resource.

// TODO: add description.

```http
// TODO: add example
```

<br><br>


### Successful `POST` requests should generate a `202` status code if the request was accepted but has not completed yet.

// TODO: add description.

```http
// TODO: add example
```

<br><br>


### Successful `POST` requests should exceptionally generate a `204` status code with `Location` header if the actual resource is not returned.

// TODO: add description.

```http
// TODO: add example
```

<br><br>


### When using `POST` requests to create resources, client must not pass the resource ID as a request input.

Resource IDs should be created and maintained by the API and returned with the response payload.

// TODO: complement description.

```http
// TODO: add example
```

<br><br>


### Consider designing `POST` operations as idempotent.

// TODO: add description

```http
// TODO: add example
```

// TODO: complement description

```http
// TODO: add example
```

<br><br>



## HTTP `PUT` Method Guidelines
The HTTP PUT method is a request method used to update or replace a resource on the server with the representation
enclosed in the request payload. It's commonly employed when the client intends to update an existing resource or
create a new one if it doesn't exist. PUT typically replaces the entire resource with the new representation provided
in the request.
<br>


### Always use `PUT` requests to update complete individual or collection resources.

// TODO: add description.

```http
// TODO: add example
```

<br><br>


### `PUT` requests should be robust against non-existence of resources by implicitly creating the resource before updating.
When clients make `PUT` requests to update a resource at a specific URI, the API should be robust against the non-existence
of the resource by implicitly creating it before performing the update. This means that if the resource identified by the
URI does not already exist, the API should create it based on the provided data in the `PUT` request payload.

**Example**:

```http
PUT /articles/123
Content-Type: application/json

{
  "title": "Updated Article",
  "content": "Updated content."
}
```

- **Request**: Attempts to update the article with ID `123`. If the article does not exist, the API should implicitly create it with the provided data.

```http
HTTP/1.1 200 OK
Content-Type: application/json

{
  "id": 123,
  "title": "Updated Article",
  "content": "Updated content.",
  "createdAt": "2024-05-15T12:00:00Z",
  "updatedAt": "2024-05-15T12:05:00Z"
}
```

- **Response**: The server responds with a `200 OK` status code, indicating that the `PUT` request was successful. If the article did not exist previously, it is created with the specified `title`, `content`, `createdAt`, and `updatedAt` timestamps. If the article already existed, it is updated with the provided data.

By implementing this guideline, an API provides flexibility and robustness in handling `PUT` requests, allowing clients
to use the same method for both creating and updating resources at specific URIs. This practice simplifies API usage,
ensures consistency and predictability in API interactions and improves the overall developer experience. However, note
that this behavior may vary based on specific use cases and API requirements.

Tags: `HTTP methods` `PUT` `resource creation` `resource update` `idempotence` `API robustness` `resource handling` `developer experience` `best practices`
<br><br>


### Always replace the entire resource addressed by the URL with the representation passed in the payload on a successful `PUT` request.

Subsequent reads of the same resource, will return the exact content that was passed to the server.

// TODO: complement description.

```http
// TODO: add example
```

<br><br>


### Successful `PUT` requests should generate a `200` status code if the resource was updated with actual content returned.

// TODO: add description.

```http
// TODO: add example
```

<br><br>


### Successful `PUT` requests should generate a `204` status code if the resource was updated without actual content returned.

// TODO: add description.

```http
// TODO: add example
```

<br><br>



## HTTP `DELETE` Method Guidelines
The HTTP DELETE method is a standard HTTP request method used to delete a specified resource on a server. When a client sends a
DELETE request, it instructs the server to remove the resource identified by the URI. This method is idempotent, meaning that
multiple identical requests have the same effect as a single request. 
<br>


### Consider generating an HTTP `200` return code on a successful `DELETE` request if the deleted resource is returned after executing the request.

// TODO: add description.

<br>


### Prefer generating an HTTP `204` return code on a successful `DELETE` request if no further information is returned after executing the request.
When no content is returned after a delete operation successfully executes, an HTTP status code 204 should be returned. This indicates that the
process has been successfully handled, however, the body of the response does not contain additional information.


### `DELETE` operations should be idempotent.
Clients should be able to make the same request repeatedly over the same resource, while resulting in the same state.

// TODO: complement description

```http
// TODO: add examples
```

See also: Idempotency
<br><br>



## HTTP `PATCH` Method Guidelines
The HTTP PATCH method is a request method used to apply partial modifications to a resource on a server. Unlike the PUT
method, which updates the entire resource, PATCH allows for more fine-grained updates, modifying only the specified parts
of the resource. This method is not necessarily idempotent, as applying the same patch multiple times can result in
different outcomes.
<br>


### Always use `PATCH` requests for updating an existing object incrementally.
`PATCH` requests are used to apply partial updates to an existing resource. Unlike `PUT` requests, which replace the entire
resource with the new data, `PATCH` requests allow clients to send only the changes or updates that need to be applied. This
makes `PATCH` ideal for scenarios where only specific fields of a resource need to be modified without affecting the entire
resource.

**Example**:

```http
PATCH /users/123
Content-Type: application/json

{
  "email": "newemail@example.com"
}
```

- **Request**: Updates the email address of the user with ID `123`. Only the `email` field is provided, indicating that this is the only field to be updated.

```http
HTTP/1.1 200 OK
Content-Type: application/json

{
  "id": 123,
  "username": "johndoe",
  "email": "newemail@example.com",
  "createdAt": "2023-01-10T08:00:00Z",
  "updatedAt": "2024-05-15T12:10:00Z"
}
```

- **Response**: The server responds with a `200 OK` status code, indicating that the `PATCH` request was successful. The response body contains the updated user resource, showing that only the `email` field was modified, while other fields remain unchanged.

Using `PATCH` for incremental updates ensures efficient use of network resources and minimizes the risk of unintentional
data loss. It allows for efficient and precise updates to resources, reducing unnecessary data transfer and
preserving the integrity of existing data. Clients can perform targeted updates without the risk of overwriting
unintended parts of a resource.

References: [RFC 5789](https://datatracker.ietf.org/doc/html/rfc5789)
<br><br>


### Consider designing `PATCH` operations as idempotent.

// TODO: add description

```http
// TODO: add example
```

// TODO: complement description

```http
// TODO: add example
```

<br><br>



## HTTP `HEAD` Method Guidelines
The HTTP HEAD method is a request method used to retrieve the headers of a specified resource, without fetching the actual
body content. When a client sends a HEAD request, the server responds with the same headers it would send for a GET request,
but without the response body. This method is useful for checking metadata, such as content type and size, or testing if a
resource exists (via the status code) without downloading the entire resource
<br>


### Always use `HEAD` requests to retrieve header information of single resource or a collections of resources.
The `HEAD` method returns the metadata of an object for a `GET` response. It is an idempotent operation.

The `HEAD` method is used to retrieve the headers of a resource without fetching the actual body. This is useful
for obtaining metadata about a resource, such as its size, content type, or last modified date, without transferring
the entire resource representation. Using `HEAD` requests can improve performance and reduce bandwidth usage, 
particularly when clients only need to check the headers before making decisions about further actions.

**Example**:

#### Example for Single Resource

```http
HEAD /articles/123
```

- **Request**: Retrieves header information for the article with ID `123`.

```http
HTTP/1.1 200 OK
Content-Type: application/json
Content-Length: 1234
Last-Modified: Mon, 15 May 2024 12:00:00 GMT
ETag: "abc123"
```

- **Response**: The server responds with the headers that describe the article with ID `123`, including `Content-Type`, `Content-Length`, `Last-Modified`, and `ETag`. The response does not include the body of the article.

#### Example for Collection of Resources

```http
HEAD /articles
```

- **Request**: Retrieves header information for the collection of articles.

```http
HTTP/1.1 200 OK
Content-Type: application/json
Content-Length: 5678
Last-Modified: Mon, 15 May 2024 12:00:00 GMT
ETag: "def456"
```

- **Response**: The server responds with headers that describe the collection of articles, including `Content-Type`, `Content-Length`, `Last-Modified`, and `ETag`. The response does not include the body of the articles collection.

The response to a `HEAD` request should be identical to that of a corresponding `GET` request, except that it does not contain a
response body.

See also: Idempotency
<br><br>


### Consider using `HEAD` to efficiently lookup whether large resources or collection resources have been updated in conjunction with the `ETag` header.

// TODO: add description.

```http
// TODO: add example
```

See also: Concurrency
<br><br>



## HTTP `OPTIONS` Method Guidelines
The HTTP OPTIONS method is a request method used to describe the communication options available for a specified resource
or the server as a whole. When a client sends an OPTIONS request, the server responds with the allowed HTTP methods (such as
GET, POST, PUT, DELETE) that can be performed on the resource. This method is useful for determining the capabilities of a
server or resource, often used in the context of Cross-Origin Resource Sharing (CORS) to check permitted operations before
making actual requests.
<br>


### Always use `OPTIONS` requests to inspect the available operations of a specific endpoint.
The `OPTIONS` method is used by a client to determine what are the communication options available for a specific resource.

```http
// TODO: add example
```

See also: HTTP Methods
<br><br>


## HTTP 'TRACE' Method Guidelines
The HTTP TRACE method is a request method used for diagnostic purposes, allowing the client to see what is being received
at the other end of the request chain and to use that data for testing or debugging. When a client sends a TRACE request,
the server echoes back the received request so the client can see any modifications or additions made by intermediate
servers. This method helps in identifying potential issues in the request path, such as changes made by proxies.
<br>


### Consider using the `TRACE` method to debug or troubleshoot web server connections.
The `TRACE` method is a useful tool for debugging and troubleshooting web server connections during the development
phase. It echoes the contents of an HTTP request back to the requester, allowing developers to see the exact request
received by the server and verify that the server is processing requests correctly.

**Usage Scenario:**
- **Development and Debugging**: During development, the `TRACE` method can help developers ensure that HTTP requests are being correctly received and processed by the server. It can reveal issues with request formatting, headers, and other request attributes.

**Security Considerations:**
- **Disable in Production**: While useful in development, the `TRACE` method should be disabled in production environments to prevent potential security risks such as Cross-Site Tracing (XST) attacks.

**Example Request and Response:**
```http
// Request
TRACE /trace HTTP/1.1
Host: example.com
User-Agent: curl/7.64.1
Accept: */*

// Response
HTTP/1.1 200 OK
Content-Type: message/http

TRACE /trace HTTP/1.1
Host: example.com
User-Agent: curl/7.64.1
Accept: */*
```

**Tags:** `debugging` `development` `HTTP methods` `TRACE` `troubleshooting` `best practices`
<br><br>


### Always disable the `TRACE` method for security reasons, unless specifically required.
The HTTP `TRACE` method should be disabled in your API to prevent potential security vulnerabilities. The
`TRACE` method is primarily used for diagnostic purposes, allowing clients to see the exact request sent to
the server and the server's response. However, it can be exploited by malicious users to access sensitive
information in HTTP headers, such as cookies and authentication tokens.

**Security Risks:**
- **Cross-Site Tracing (XST) Attacks**: Attackers can exploit `TRACE` to steal credentials or session information by tricking the client into sending a request that reveals sensitive data.
- **Information Leakage**: `TRACE` can expose internal implementation details and HTTP headers that should remain confidential.

**Example Request and Response:**
```http
// Request
TRACE /api/resource HTTP/1.1
Host: example.com

// Response (when TRACE is disabled)
HTTP/1.1 405 Method Not Allowed
Content-Type: application/json

{
  "error": "Method Not Allowed",
  "message": "The TRACE method is disabled for security reasons."
}
```

**Tags:** `security` `HTTP methods` `TRACE` `vulnerability` `best practices`
<br><br>



## HTTP Status Codes Guidelines
<br>


### Always use the most specific HTTP status codes for returning information regarding request and error handling.
When returning information to clients regarding request or error handling, the API should use the most specific 
HTTP status code possible. This practice ensures clear communication between the server and the client, helping
clients understand the exact nature of the response and how to handle it appropriately.

**Benefits of Using Specific HTTP Status Codes:**
- **Clarity**: Specific status codes provide precise information about the outcome of the request, reducing ambiguity.
- **Troubleshooting**: Clear status codes make it easier to diagnose issues and understand the cause of errors.
- **Client Handling**: Clients can implement more accurate error handling and responses based on specific status codes.

**Examples:**
- **400 Bad Request**: Use when the request cannot be processed due to client-side errors, such as validation issues.
  ```http
  HTTP/1.1 400 Bad Request
  Content-Type: application/json

  {
    "error": "Bad Request",
    "message": "Invalid input data"
  }
  ```
- **401 Unauthorized**: Use when authentication is required and has failed or not been provided.
  ```http
  HTTP/1.1 401 Unauthorized
  Content-Type: application/json

  {
    "error": "Unauthorized",
    "message": "Authentication required"
  }
  ```
- **404 Not Found**: Use when the requested resource could not be found.
  ```http
  HTTP/1.1 404 Not Found
  Content-Type: application/json

  {
    "error": "Not Found",
    "message": "Resource not found"
  }
  ```

**Tags:** `HTTP status codes` `error handling` `client communication`
<br><br>


### Always use HTTP `4XX` return codes for malformed requests, when the issue is on the client's side.
HTTP `4XX` status codes should always be used to indicate that a request is malformed or cannot be processed due
to issues on the client's side. These status codes inform the client that the server has understood the request,
but it cannot process it due to client-related errors. 

**Key Points for Using `4XX` Status Codes:**

- **Client-Side Errors:** `4XX` status codes are specifically designed to signal issues that originate from the client's side, such as invalid input data, unauthorized access attempts, or requests for non-existent resources.
  
- **Error Clarification:** Each `4XX` status code provides specific information about the type of client-side error, helping clients quickly identify and rectify the issue.

- **Common `4XX` Codes:**
  - **400 Bad Request**: Indicates that the server cannot process the request due to malformed syntax, invalid input data, or other client-side issues.
  - **401 Unauthorized**: Signals that authentication is required and has failed or is not provided.
  - **403 Forbidden**: Indicates that the client is authenticated but does not have permission to access the requested resource.
  - **404 Not Found**: Used when the requested resource cannot be found on the server.
  - **409 Conflict**: Indicates that the request could not be processed due to a conflict with the current state of the resource.

**Benefits:**
- **Clear Communication:** Using the appropriate `4XX` status code ensures that the client is clearly informed about the specific nature of the error, which helps in understanding and resolving the issue.
- **Enhanced Client-Side Handling:** Precise status codes enable the client to implement more effective error handling and user notifications, improving the overall user experience.

<br><br>


### Consider using an HTTP `429` return code when a client breaks a request rate limit.

// TODO: add description.

```http
// TODO: add example
```

See also: HTTP Methods
<br><br>


### Always use HTTP `5XX` return codes for internal errors, when the issue is on the API's side.

// TODO: add description.

```http
// TODO: add example
```

See also: HTTP Methods
<br><br>


