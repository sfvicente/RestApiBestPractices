# Filtering


## General
<br>


### Always respond with a valid response body and a `200` HTTP status code when filtering is performed on a collection and the result set is empty.

// TODO: add description

```http
GET https://api.myapi.com/orders?$filter=...
Accept: application/json

HTTP/1.1 200 OK
Content-Type: application/json

{
  ...,
  "value": []
}
```

// TODO: complement description

```http
// TODO: add example
```

<br><br>


### Always use query parameters to allow clients to filter resources

// TODO: add description

```http
GET /api/products?category=electronics
```

<br><br>


### Consider allowing the combination of multiple filter criteria using logical operators

// TODO: add description

```http
GET /api/products?category=electronics&price<100
```

<br><br>


### Always use clear and consistent syntax for filter expressions

// TODO: add description

```http
GET /api/products?price[lt]=100&price[gt]=10
```

<br><br>


### Always provide comprehensive documentation listing all available filters, their data types, and usage examples

// TODO: add description

```http
// TODO: add example
```

<br><br>


### Consider limit the number of filter combinations to avoid performance issues

// TODO: add description

```http
// TODO: add example
```

Tags: `performance`
<br><br>


### Always define and document the default filtering behavior when no filter parameters are specified

// TODO: add description

```http
// TODO: add example
```

<br><br>


### Always validate and sanitize filter inputs to prevent SQL injection and other security vulnerabilities

// TODO: add description

```http
// TODO: add example
```

Tags: `security`
<br><br>


### Consider combining filtering with pagination to manage large datasets

// TODO: add description

```http
GET /api/products?category=electronics&page=2&size=20
```

Tags: `pagination`
<br><br>


### Consider allowing range queries for numerical and date fields

// TODO: add description

**Request**
```http
GET /api/products?price[gte]=10&price[lte]=100
```

<br><br>


### Consider providing sorting options along with filtering

// TODO: add description

**Request**
```http
GET /api/products?category=electronics&sort=price,asc
```

Tags: `sorting`
<br><br>


### Always return 200 OK for successful filtered requests, even when the result set is empty.
When processing a request that involves filtering resources, the server should always return a `200 OK` status code if the
request is successful, regardless of whether the filtered result set contains any resources. This approach ensures consistency
in API responses and provides clear feedback to the client that the request was processed successfully without any errors.

Returning a `200 OK` status code for an empty result set distinguishes between an empty but valid response and an error
condition. An empty result set is a valid outcome for a request where no resources match the specified criteria.

**Example:**

If a client sends a request to retrieve a list of articles filtered by a specific tag, but there are no articles with
that tag, the server should return a `200 OK` status code with an empty array in the response body.

**Request**
```http
GET /articles?tag=nonexistent-tag
```

- **Request**: Attempts to retrieve articles with a specific tag that does not exist in the database.

**Response**
```http
HTTP/1.1 200 OK
Content-Type: application/json

[]
```

- **Response**: The server responds with a `200 OK` status code, indicating that the request was successful. The response body contains an empty array, signifying that no articles matched the specified tag.

<br><br>


### Always return `400 Bad Request` for invalid filter parameters

// TODO: add description

**Request**
```http
// TODO: add example
```

<br><br>


### Consider including metadata such as the total number of filtered items, current page, and page size in the response

// TODO: add description

**Request**
```http
// TODO: add example
```

<br><br>


### Consider allowing case insensitive filtering for string fields to improve usability

// TODO: add description

**Request**
```http
// TODO: add example
```

<br><br>


### Consider implementing caching strategies for commonly used filters to enhance performance

// TODO: add description

**Request**
```http
// TODO: add example
```

Tags: `caching`
<br><br>


### Always follow consistent naming conventions for query parameters across the API to improve usability and readability

// TODO: add description

**Request**
```http
// TODO: add example
```

Tags: `naming conventions` `query parameters` `usability` `readability`
<br><br>