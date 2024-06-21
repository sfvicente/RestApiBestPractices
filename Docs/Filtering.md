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