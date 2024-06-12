# HTTP Status Codes


## General
<br>


### Prefer the use of standard HTTP status codes to represent the outcome of API requests clearly.

// TODO: add description

```http
// TODO: add example
```

// TODO: complement description

```http
// TODO: add example
```

<br><br>


### Ensure consistency in status codes across the entire API to avoid confusion.

// TODO: add description

```http
// TODO: add example
```

// TODO: complement description

```http
// TODO: add example
```

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


## `2xx` Status Codes
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

**Request for Creating a New Resource**
```http
POST /articles
Content-Type: application/json

{
  "title": "New Article",
  "content": "Lorem ipsum dolor sit amet, consectetur adipiscing elit."
}
```

**Response**
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

Additional Tags: `location`
<br><br>


### Consider using `202 Accepted` for asynchronous operations where the request has been accepted but processing is not yet complete.


// TODO: add description

```http
// TODO: add example
```

// TODO: complement description

```http
// TODO: add example
```

<br><br>


### Always return `204 No Content` for successful `DELETE` requests or `PUT` requests when no content is returned.

// TODO: add description

```http
// TODO: add example
```

// TODO: complement description

```http
// TODO: add example
```

<br><br>


### Always return `206 Partial Content` when serving partial GET requests to support range queries for large resources.

// TODO: add description

```http
// TODO: add example
```

// TODO: complement description

```http
// TODO: add example
```

<br><br>


## `3xx` Status Codes
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

// TODO: add description

```http
// TODO: add example
```

// TODO: complement description

```http
// TODO: add example
```

<br><br>


### Always use `302 Found` for temporary redirections when a resource is temporarily available at a different URL.

// TODO: add description

```http
// TODO: add example
```

// TODO: complement description

```http
// TODO: add example
```

<br><br>


### Use `303 See Other` to redirect after a POST request, directing the client to retrieve the resource at a different URL.

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


### Always implement `307 Temporary Redirect` to preserve the original HTTP method while redirecting to a temporary URL.

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


### Always use `308 Permanent Redirect` to preserve the original HTTP method while redirecting to a permanent URL.

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


## `4xx` Status Codes
The 4xx class of HTTP status codes indicates that the client seems to have made an error. These codes are meant
to inform the client about issues with the request.

### Always use `400 Bad Request` for requests that cannot be processed due to client-side errors.

// TODO: add description

```http
// TODO: add example
```

// TODO: complement description

```http
// TODO: add example
```

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


### Always use `403 Forbidden` when the client is authenticated but does not have permission to access the resource.

// TODO: add description

```http
// TODO: add example
```

// TODO: complement description

```http
// TODO: add example
```

See also: `security` `authorization`
<br><br>


### Always return `404 Not Found` when a requested resource cannot be found on the server.

// TODO: add description

```http
// TODO: add example
```

// TODO: complement description

```http
// TODO: add example
```

<br><br>


### Always use `405 Method Not Allowed` when the HTTP method used is not supported by the resource.

// TODO: add description

```http
// TODO: add example
```

// TODO: complement description

```http
// TODO: add example
```

<br><br>


### Always return 409 Conflict when a request could not be processed due to a conflict with the current state of the resource.

// TODO: add description

```http
// TODO: add example
```

// TODO: complement description

```http
// TODO: add example
```

<br><br>


### Always use `410 Gone` for resources that have been permanently removed and will not be available again.

// TODO: add description

```http
// TODO: add example
```

// TODO: complement description

```http
// TODO: add example
```

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


## `5xx` Status Codes
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

// TODO: add description

```http
// TODO: add example
```

// TODO: complement description

```http
// TODO: add example
```

<br><br>


### Return `502 Bad Gateway` when the server, acting as a gateway or proxy, receives an invalid response from an inbound server.

// TODO: add description

```http
// TODO: add example
```

// TODO: complement description

```http
// TODO: add example
```

<br><br>


### Always use `503 Service Unavailable` when the server is temporarily unable to handle the request, often due to maintenance or overloading.

// TODO: add description

```http
// TODO: add example
```

// TODO: complement description

```http
// TODO: add example
```

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


### Always use `505 HTTP Version Not Supported` when the server does not support the HTTP protocol version used in the request.

// TODO: add description

```http
// TODO: add example
```

// TODO: complement description

```http
// TODO: add example
```

<br><br>



### Always use `511 Network Authentication Required` when the client needs to authenticate to gain network access.

// TODO: add description

```http
// TODO: add example
```

// TODO: complement description

```http
// TODO: add example
```

See Also: `authentication`
<br><br>


