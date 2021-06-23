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
