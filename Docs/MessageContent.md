# Message Content
 Message Content refers to the data included in the body of an HTTP request or response. This content conveys the actual
 information being transferred between the client and the server.



## Data Structure
<br>

### Always maintain consistent data structures across endpoints to ensure predictable responses

// TODO: complement description

```http
// TODO: add example
```

<br><br>


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


### Always include the `Content-Type` header in the responses to specify the format of the returned data

// TODO: complement description

```http
// TODO: add example
e.g., Content-Type: application/json.
```

Tags: `Content-Type`
<br><br>


### Consider allowing clients to request different data formats using the `Accept` header

// TODO: complement description

```http
// TODO: add example
such as XML or CSV if needed. 
```

Tags: `Accept`
<br><br>


### Always provide JSON as the default response format
To ensure consistency, interoperability, and ease of use, services should always provide JSON as the default encoding format for data
exchange. JSON is lightweight, human-readable, and widely supported across different programming languages, making it an ideal choice
for modern web APIs. By adopting JSON as the default response format, services offer a standardized and familiar structure for developers
interacting with the API.

While supporting multiple formats such as XML or YAML can be useful in certain cases, JSON should be the default due to its simplicity
and efficiency. If a client requires a different response format, the API should allow negotiation via the `Accept` header, but JSON
remains the fallback option.

**Example**:

```http
GET /api/users HTTP/1.1
Host: example.com
Accept: application/json
```

- **Request**: The client requests a list of users in JSON format.

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

- **Response**: The server responds with a `200 OK` status code and provides the user data in JSON format, the default encoding. 

Tags: `response format` `JSON` `content negotiation` `interoperability` `default behavior` `data exchange`
<br><br>


## JSON Data
<br>


### Consider following camel case naming conventions for JSON property names

e.g., firstName instead of first_name.

// TODO: complement description

```http
// TODO: add example
```

<br><br>


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


