# HTTP Headers
HTTP headers are the name or value pairs containing additional information that are transferred between clients and servers
with HTTP requests or responses.
<br>


## General
<br>


### Consider using standardized headers.

// TODO: add description

```http
// TODO: add example
```

// TODO: complement description

```http
// TODO: add example
```

<br><br>


## `Prefer` Header
The Prefer header is an HTTP request header used by clients to indicate their preferred server behaviors in processing
the request. It allows clients to suggest specific handling instructions without altering the fundamental request semantics.
<br>


### Consider supporting the `Prefer` header to handle processing preferences.
Implement support for the `Prefer` header to allow clients to indicate their processing preferences. This enhances flexibility and
responsiveness by enabling the server to tailor its behavior based on client requirements.

**Client Request**
```http
POST /api/orders
Prefer: return=representation
Content-Type: application/json

{
  "product_id": 123,
  "quantity": 2
}
```

**Server Response**
```http
HTTP/1.1 201 Created
Content-Type: application/json
Preference-Applied: return=representation

{
  "order_id": 789,
  "product_id": 123,
  "quantity": 2,
  "status": "confirmed"
}
```

**Scenarios**
- Response Content: When clients prefer the server to include the created resource in the response after a `POST` request (`Prefer: return=representation`).
- Minimal Responses: When clients prefer to receive a minimal response without the resource representation (`Prefer: return=minimal`).
- Asynchronous Processing: When clients indicate they prefer the server to process the request asynchronously if possible (`Prefer: respond-async`).
- Wait Time Specification: When clients specify a maximum wait time for the response using `Prefer: wait=<seconds>`, indicating the server should prioritize responding within the given time frame.
- Handling Conflicts: When clients request that conflicts should be handled without returning an error using `Prefer: handling=lenient`, allowing the server to take alternative actions to fulfill the request.

To implement support for the `Prefer` header:
- Inspect the `Prefer` header in the client request to determine the specified preference.
- Apply the preference and adjust the server's response accordingly.
- Include the `Preference-Applied` header in the response to indicate that the preference has been honored.
- Ensure that unsupported preferences are gracefully ignored, maintaining standard behavior.

Supporting the `Prefer` header allows clients to communicate their preferences, leading to more efficient and tailored interactions, and
improving overall user experience.

Tags: `headers` `Prefer` `processing preferences` `flexibility`
<br><br>


## Custom Headers
Custom headers in HTTP are non-standard headers used to pass additional information between the client and the
server. These headers are typically defined by the developer and are used to meet specific application requirements
that are not covered by standard HTTP headers.
<br>


### Do not require custom headers for operating basic functionality of an API.

// TODO: add description

```http
// TODO: add example
```

// TODO: complement description

```http
// TODO: add example
```

<br><br>


### Consider using custom headers when services require additional functionality which is exposed via HTTP headers.

// TODO: add description

```http
// TODO: add example
```

// TODO: complement description

```http
// TODO: add example
```

<br><br>


### Prefix custom header names with `X-` for legacy systems or use clear, application-specific names.

// TODO: add description

```http
// TODO: add example
```

// TODO: complement description

```http
// TODO: add example
```

<br><br>


### Ensure custom headers are well-documented for ease of use and integration.

// TODO: add description

```http
// TODO: add example
```

// TODO: complement description

```http
// TODO: add example
```

<br><br>


### Validate custom header values on both client and server sides to maintain data integrity.

// TODO: add description

```http
// TODO: add example
```

// TODO: complement description

```http
// TODO: add example
```

<br><br>


### Keep custom header names concise yet descriptive to enhance readability.

// TODO: add description

```http
// TODO: add example
```

// TODO: complement description

```http
// TODO: add example
```

<br><br>


### Use custom headers to convey metadata that does not fit within the standard headers.

// TODO: add description

```http
// TODO: add example
```

// TODO: complement description

```http
// TODO: add example
```

<br><br>


### Avoid exposing sensitive information in custom headers to enhance security.

// TODO: add description

```http
// TODO: add example
```

// TODO: complement description

```http
// TODO: add example
```

See also: Security
<br><br>


### Ensure custom headers comply with security protocols, such as encryption when necessary.

// TODO: add description

```http
// TODO: add example
```

// TODO: complement description

```http
// TODO: add example
```

See also: Security
<br><br>


### Leverage custom headers for request tracing and logging to improve debugging capabilities.

// TODO: add description

```http
// TODO: add example
```

// TODO: complement description

```http
// TODO: add example
```

See also: Security
<br><br>


### Implement custom header support in a backward-compatible manner.

// TODO: add description

```http
// TODO: add example
```

// TODO: complement description

```http
// TODO: add example
```

See also: compatibility
<br><br>


### Minimize performance overhead by optimizing the processing of custom headers.

// TODO: add description

```http
// TODO: add example
```

// TODO: complement description

```http
// TODO: add example
```

See also: performance
<br><br>


### Test custom headers thoroughly across different clients and environments to ensure consistency

// TODO: add description

```http
// TODO: add example
```

// TODO: complement description

```http
// TODO: add example
```

See also: testing
<br><br>


### Handle errors gracefully when custom headers are missing or malformed.

// TODO: add description

```http
// TODO: add example
```

// TODO: complement description

```http
// TODO: add example
```

See also: `error handling`
<br><br>


### Follow industry standards and best practices for naming and using custom headers to enhance interoperability.

// TODO: add description

```http
// TODO: add example
```

// TODO: complement description

```http
// TODO: add example
```

See also: interoperability
<br><br>