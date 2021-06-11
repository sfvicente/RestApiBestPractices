# HTTP Communication


## General

...





## HTTP `GET` method

<br>


### Always use `GET` requests to read a single resource or a collection of resources.

<br>


### `GET` requests for individual resources that do not exist should generate a `404`.

// TODO: add description.

```http
// TODO: add example
```

<br><br>


### `GET` requests for collection resources should return `200` if the collection is empty.

// TODO: add description.

```http
// TODO: add example
```

<br><br>


### GET requests for collection resources should return `404` if the collection is missing.

// TODO: add description.

```http
// TODO: add example
```

<br><br>


### `GET` requests on collection resources should provide adequate filter and pagination mechanisms.

// TODO: add description.

```http
// TODO: add example
```

See also: Filtering, Pagination
<br><br>



## HTTP `POST` method

<br>


### Successful `POST` requests should generate a `200` status code if resources have been updated.

// TODO: add description.

```http
// TODO: add example
```

<br><br>


### Successful `POST` requests should generate a `201` status code if resources have been created.

// TODO: add description.

```http
// TODO: add example
```

<br><br>



## HTTP `DELETE` Method

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


## HTTP `HEAD` Method
<br>


### Always use `HEAD` requests to retrieve header information of single resource or a collections of resources.

// TODO: add description.

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

