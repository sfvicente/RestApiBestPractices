# Operations
When designing a RESTful API, operations refer to the actions that can be performed on resources exposed by the API. These
operations are mapped to specific HTTP methods to convey the intent of the client's request and to adhere to the principles
of the HTTP protocol.
<br>

## General
<br>


### API operations should be defined in terms of HTTP methods
API operations should be defined using the appropriate HTTP methods to leverage the semantics and behaviors defined
by the HTTP protocol. Each HTTP method corresponds to a specific action or intent, providing a standardized and 
intuitive approach to interacting with RESTful APIs.

- **Semantic Clarity**: HTTP methods convey the intent of an API request (e.g., retrieving data, creating resources, updating resources, deleting resources) in a clear and standardized manner.
- **Idempotent and Safe Operations**: HTTP methods like `GET`, `PUT`, and `DELETE` have defined idempotent and safe characteristics, aligning with REST principles.
- **Uniform Interface**: Leveraging HTTP methods establishes a uniform interface for API endpoints, improving consistency and predictability.

<sub>See also: HTTP Methods</sub>
<br><br>


### Always use `GET` for retrieving resources without side effects
The `GET` method should exclusively be used for fetching data or resources from the server. It must be idempotent and free of side effects, meaning
it should not modify, create, or delete any data on the server. This ensures that clients can safely repeat `GET` requests without concerns about
changing the state of the resource.

In adherence to REST principles, `GET` operations should be simple and focused solely on reading or retrieving information.

```http
GET /api/users HTTP/1.1
Host: example.com
Accept: application/json
```

- **Request**: Retrieves a list of users from the API.

```http
HTTP/1.1 200 OK
Content-Type: application/json

[
  {
    "id": 1,
    "username": "janedoe",
    "email": "jane@example.com"
  },
  {
    "id": 2,
    "username": "johndoe",
    "email": "john@example.com"
  }
]
```

- **Response**: The server returns a `200 OK` status code and a JSON array with the user data (`id`, `username`, `email`). This is a basic read-only operation that retrieves data without modifying the server.

<sub>See also: HTTP Methods</sub>
<br><br>


### Always use `POST` for creating new resources
Use the `POST` method to create new resources on the server. `POST` requests are designed for operations where the client submits data that
the server uses to generate new resources. These requests should be non-idempotent, meaning each request results in the creation of a new
resource, even if the data is identical to previous submissions. 

A `POST` request typically returns a `201 Created` status code, along with a `Location` header containing the URI of the newly created
resource. The response body may include a representation of the resource itself.

**Example:**

```http
POST /api/users HTTP/1.1
Host: example.com
Content-Type: application/json

{
  "username": "janedoe",
  "email": "jane@example.com"
}
```

- **Request**: Creates a new user with the provided `username` and `email`.

```http
HTTP/1.1 201 Created
Content-Type: application/json
Location: /api/users/1

{
  "id": 1,
  "username": "janedoe",
  "email": "jane@example.com",
  "createdAt": "2024-09-06T12:00:00Z"
}
```

- **Response**: The server returns a `201 Created` status code and the `Location` header pointing to the new resource’s URI (`/api/users/1`). The response body contains the newly created user data, including the `id` and `createdAt` timestamp.

<sub>See also: HTTP Methods</sub>
<br><br>


### Consider supporting partial responses for large binary resources
When handling larger binary resources, such as images or videos, consider implementing support for partial responses using the `Range` header. This
allows clients to request specific portions of a resource, improving performance and reducing bandwidth usage. It is particularly useful when
downloading large files, streaming content, or when network reliability is a concern.

Supporting partial responses ensures that large resources can be retrieved incrementally, minimizing the load on both the client and server.

**Example:**

```http
GET /files/video.mp4 HTTP/1.1
Host: example.com
Range: bytes=0-999
```

- **Request**: The client requests the first 1000 bytes (from byte 0 to 999) of the file `video.mp4`.

```http
HTTP/1.1 206 Partial Content
Content-Type: video/mp4
Content-Range: bytes 0-999/5000000

(binary data)
```

- **Response**: The server responds with a `206 Partial Content` status code, indicating that the requested range of the resource is being returned. The `Content-Range` header specifies which portion of the resource is included, and the total size of the file (`5000000` bytes).

See also: Binary Resources, Performance
<br><br>


### Consider implementing HTTP `HEAD` requests for large binary resources
When dealing with large binary resources, such as images, videos, or files, consider implementing support for HTTP `HEAD` requests. The `HEAD` method
is useful when clients need metadata about a resource, like its size, content type, or last modified date, without downloading the entire file. This
can help clients decide whether to proceed with a `GET` request, especially for large resources, improving efficiency and reducing unnecessary bandwidth usage.

The `HEAD` request returns the same headers as a `GET` request but without the response body, making it an effective way to retrieve resource information.

**Example:**

```http
HEAD /files/video.mp4 HTTP/1.1
Host: example.com
```

- **Request**: The client sends a `HEAD` request to get metadata about the `video.mp4` file.

```http
HTTP/1.1 200 OK
Content-Type: video/mp4
Content-Length: 5000000
Last-Modified: Wed, 15 May 2024 12:00:00 GMT
```

- **Response**: The server responds with headers that include the content type (`video/mp4`), the content length (`5000000` bytes), and the last modified date. No body is returned in the response.

Tags: `HTTP methods` `HEAD` `binary resources` `metadata` `performance optimization` `content length` `file handling` `large resources` `efficiency`
<br><br>
