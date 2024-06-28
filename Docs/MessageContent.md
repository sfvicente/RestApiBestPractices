# Message Content
 Message Content refers to the data included in the body of an HTTP request or response. This content conveys the actual
 information being transferred between the client and the server.


## Data Formats
<br>


### Always implement content negotiation using the `Accept` header to allow clients to specify their preferred response format

// TODO: complement description

```http
// TODO: add example
```

<br><br>


### Consider optimizing the size of the payload by excluding unnecessary data and using efficient data formats

// TODO: complement description

```http
// TODO: add example
```

<br><br>


### Always implement data validation and sanitation to ensure that incoming data adheres to expected formats and prevent security vulnerabilities

// TODO: complement description

```http
// TODO: add example
```

<br><br>


### Consider ensuring support for UTF-8 encoding for all text data to handle international characters correctly

// TODO: complement description

```http
// TODO: add example
```

<br><br>


### Consider using ISO 8601 format to handle dates and times fields appropriately

// TODO: complement description

```http
// TODO: add example
```

<br><br>


### Always use JSON as the payload data interchange format.

// TODO: add description

```http
// TODO: add example
```

// TODO: complement description

```http
// TODO: add example
```

<br><br>


### Service operations should provide JSON as the default encoding.

// TODO: add description

```http
// TODO: add example
```

// TODO: complement description

```http
// TODO: add example
```

<br><br>


## JSON Data
<br>


### Property names should use snake case.

// TODO: add description

```http
// TODO: add example
```

// TODO: complement description

```http
// TODO: add example
```

<br><br>


### Object names should be singular.

// TODO: add description

```http
// TODO: add example
```

// TODO: complement description

```http
// TODO: add example
```

<br><br>


### Do not use `null` for boolean properties.

// TODO: add description

```http
// TODO: add example
```

// TODO: complement description

```http
// TODO: add example
```

<br><br>


### Prefer the use of enumerations of named values instead of nullable boolean properties.

// TODO: add description

```http
// TODO: add example
```

// TODO: complement description

```http
// TODO: add example
```


### Array names should be pluralized.

// TODO: add description

```http
// TODO: add example
```

// TODO: complement description

```http
// TODO: add example
```

<br><br>


### Prefer the use of the empty list representation instead of `null` for empty arrays.

// TODO: add description

```http
// TODO: add example
```

// TODO: complement description

```http
// TODO: add example
```

<br><br>


### Do not perform date localization in the API

When localization of dates is required on client applications, it should be performed by those applications not the API.

// TODO: add description

```http
// TODO: add example
```

// TODO: complement description

```http
// TODO: add example
```

<br><br>


### Always use `Base64` encoding or other appropriate methods to handle binary data within JSON or other text-based formats

// TODO: complement description

```http
// TODO: add example
```

<br><br>


