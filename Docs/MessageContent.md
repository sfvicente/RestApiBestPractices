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
Content negotiation allows clients to specify the desired format for the response data using the `Accept` header. This ensures that
the server can dynamically return the response in the format requested by the client, such as `application/json`, `application/xml`,
or `text/plain`. If the server supports multiple formats, it can respond with the best match based on the `Accept` header values
provided by the client.

Implementing content negotiation improves flexibility, allowing the same API to serve different clients with varying format
requirements, while maintaining consistent behavior.

**Example:**

```http
GET /api/users HTTP/1.1
Host: example.com
Accept: application/json
```

- **Request**: The client requests a list of users in JSON format by specifying `Accept: application/json`.

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

- **Response**: The server responds with the requested JSON data and includes the `Content-Type: application/json` header to indicate the format of the response.

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
The `Content-Type` header in HTTP responses informs the client about the format of the returned data, allowing proper
interpretation. This header specifies the media type (MIME type) of the response body, such as `application/json` for
JSON data or `text/html` for HTML.

Always setting the `Content-Type` ensures that clients can correctly process the response, avoiding potential errors or
misinterpretations. It's particularly important in APIs where different response formats may be supported, or where the
client needs to parse the response in a specific way.

**Example:**

```http
HTTP/1.1 200 OK
Content-Type: application/json

{
  "id": 1,
  "username": "janedoe",
  "email": "jane@example.com"
}
```

- **Response**: The server includes the `Content-Type: application/json` header, indicating the data is formatted in JSON. The client will use this information to correctly parse the returned user data.

Tags: `Content-Type Header` `Response Format` `MIME Type` `HTTP Headers` `Data Interpretation` `Client-Server Communication` `JSON`
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


### Consider using snake case for property names

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
Methods like `Base64` encoding should be used when transmitting binary data, such as images or files, in APIs. Since JSON is text-based
and doesn’t natively support binary data, encoding the binary content into `Base64` converts it into a text format that can be safely
transmitted within JSON payloads or other text-based formats.

While `Base64` encoding is the most commonly used approach, alternative methods such as `hexadecimal` encoding can also be appropriate
depending on the context. The goal is to ensure data integrity during transmission and avoid potential issues that arise from attempting
to send raw binary data in formats that are not designed for it.

Using encoding techniques like `Base64` allows APIs to handle binary data efficiently while adhering to the constraints of text-based formats.

**Example:**

```http
POST /api/upload-image HTTP/1.1
Host: example.com
Content-Type: application/json

{
  "filename": "image.png",
  "filedata": "iVBORw0KGgoAAAANSUhEUgAAAoAAAAHgCAYAAADhdbDkAA..."
}
```

- **Request**: In this example, the `filedata` field contains a `Base64`-encoded version of an image file (`image.png`). The binary image data is converted to `Base64` to be safely transmitted in the JSON payload.

```http
HTTP/1.1 201 Created
Content-Type: application/json

{
  "message": "Image uploaded successfully",
  "fileUrl": "https://example.com/images/1"
}
```

- **Response**: The server processes the `Base64`-encoded image data and returns a success message, along with the URL of the uploaded image.

Tags: `Base64 Encoding` `Binary Data Handling` `JSON` `Text-Based Formats` `Data Transmission` `Encoding Methods` `File Upload` `Data Integrity`
<br><br>


