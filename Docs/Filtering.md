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


### Always return `200 OK` for successful requests, even if the filtered result set is empty

// TODO: add description

**Request**
```http
// TODO: add example
```

<br><br>


### Always return `400 Bad Request` for invalid filter parameters

// TODO: add description

**Request**
```http
// TODO: add example
```

<br><br>
