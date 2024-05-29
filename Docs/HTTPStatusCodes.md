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


## Status Codes
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

See also: `security` `authorization`
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