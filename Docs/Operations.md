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


### Use `GET` for Read Operations
Use the `GET` method to retrieve data or resources from the server. `GET` requests should not have side effects on the server
and should only be used for retrieving data.

```http
GET /api/users HTTP/1.1
```

<sub>See also: HTTP Methods</sub>
<br><br>


### Use `POST` for Create Operations
Use the `POST` method to create new resources on the server. `POST` requests should be used for operations that result in the
creation of a new resource.

  ```http
  POST /api/users HTTP/1.1
  ```

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
