# HTTP Communication
HTTP communication in the context of REST APIs involves using standard HTTP methods, also known as verbs, to perform
operations on resources identified by URLs. Each HTTP verb provides a specific action, making REST APIs intuitive and
enabling clear, predictable interactions between clients and servers.

## General

...





## HTTP `GET` method
The HTTP GET method is a request method used to retrieve data from a specified resource on the server. It's one of the
most commonly used HTTP methods and is primarily used for fetching information. When a client sends a GET request to a
server, it typically includes parameters in the URL to specify the resource to retrieve or query parameters to filter the results.
<br>


### Always use `GET` requests to read a single resource or a collection of resources.


For retrieving a specific resource:

```http
GET /comments/:id
```


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

<br><br>


### `GET` requests on collection resources should provide adequate filter and pagination mechanisms.

// TODO: add description.

```http
// TODO: add example
```

See also: Filtering, Pagination
<br><br>



## HTTP `POST` method
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

See also: `Location` Header
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

See also: `Location` Header
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



## HTTP `PUT` Method
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



## HTTP `DELETE` Method
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



## HTTP `PATCH` Method
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



## HTTP `HEAD` Method
<br>


### Always use `HEAD` requests to retrieve header information of single resource or a collections of resources.

The `HEAD` method returns the metadata of an object for a `GET` response. It is an idempotent operation.

// TODO: complement description.

```http
// TODO: add example
```

See also: Idempotency
<br><br>


### Consider using `HEAD` to efficiently lookup whether large resources or collection resources have been updated in conjunction with the `ETag` header.

// TODO: add description.

```http
// TODO: add example
```

See also: Concurrency
<br><br>



## HTTP `OPTIONS` Method
<br>


### Always use `OPTIONS` requests to inspect the available operations of a specific endpoint.

The `OPTIONS` method is used by a client to determine what are the communication options available for a specific resource.

```http
// TODO: add example
```

See also: HTTP Methods
<br><br>


## HTTP 'TRACE' Method
<br>


### Consider using the `TRACE` method to debug or troubleshoot web server connections.

The TRACE method is used to echo the contents of an HTTP Request back to the requester which can be used for debugging purpose at the time of development.

```http
// TODO: add example
```

See also: HTTP Methods
<br><br>


### Always disable the `TRACE` method for security reasons, unless specifically required.

It is possible that malicious users, even without priviledges, can abuse the HTTP `TRACE` functionality as it allows access to HTTP headers sensitive information.

```http
// TODO: add example
```

See also: HTTP Methods
<br><br>



## HTTP Status Codes
<br>


### Always use the most specific HTTP status codes for returning information regarding request and error handling.

When returning information to clients regarding request or error handling, the API should use the most specific HTTP status code possible.

// TODO: complement description

```http
// TODO: add examples
```

See also: HTTP Status Codes
<br><br>


### Always use HTTP `4XX` return codes for malformed requests, when the issue is on the client's side.

// TODO: add description.

```http
// TODO: add example
```

See also: HTTP Methods
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


