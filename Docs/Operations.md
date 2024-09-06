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


### Consider supporting partial responses for larger binary resources
Depending on business requirements, resources may contain larger binary assets. For example, a user profile resource might contain a
binary image representation.

```http
// TODO: add example
```

// TODO: complement description

```http
// TODO: add example
```

See also: Binary Resources, Performance
<br><br>


### Consider implementing HTTP `HEAD` requests for large binary resources.

// TODO: add description

```http
// TODO: add example
```

See also: Binary Resources, Performance
<br><br>
