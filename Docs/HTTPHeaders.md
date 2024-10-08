# HTTP Headers
HTTP headers are the name or value pairs containing additional information that are transferred between clients and servers
with HTTP requests or responses.
<br>


## General Guidelines
<br>


### Consider using standardized headers

// TODO: add description

```http
// TODO: add example
```

// TODO: complement description

```http
// TODO: add example
```

<br><br>


## `Prefer` Header Guidelines
The Prefer header is an HTTP request header used by clients to indicate their preferred server behaviors in processing
the request. It allows clients to suggest specific handling instructions without altering the fundamental request semantics.
<br>


### Consider supporting the `Prefer` header to handle processing preferences
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


## Custom Headers Guidelines
Custom headers in HTTP are non-standard headers used to pass additional information between the client and the
server. These headers are typically defined by the developer and are used to meet specific application requirements
that are not covered by standard HTTP headers.
<br>


### Avoid requiring custom headers for basic API functionality

// TODO: add description

```http
// TODO: add example
```

// TODO: complement description

```http
// TODO: add example
```

<br><br>


### Consider using custom headers when services require additional functionality which is exposed via HTTP headers

// TODO: add description

```http
// TODO: add example
```

// TODO: complement description

```http
// TODO: add example
```

<br><br>


### Consider prefixing custom header names with `X-` for legacy systems or use clear, application-specific names
When defining custom headers, use the `X-` prefix for legacy systems or opt for clear, application-specific names. This
practice helps to avoid conflicts with standard HTTP headers and ensures better clarity and maintainability.

**Client Request**
```http
GET /api/data
X-Custom-Auth: abc123
```

**Server Response**
```http
HTTP/1.1 200 OK
Content-Type: application/json
X-Request-ID: 456def

{
  "data": "Sample response data"
}
```

**Scenarios**
- Authentication: When adding a custom header for authentication, such as `X-Custom-Auth`, to pass API keys or tokens in legacy systems.
- Request Tracking: When using a custom header like `X-Request-ID` to track and correlate requests and responses across different services.
- Application-Specific Data: When including application-specific information in headers, such as `App-Client-Version` to indicate the version of the client application making the request.

To implement custom headers:
- Use the `X-` prefix for headers in legacy systems where backward compatibility is essential.
- For modern applications, prefer clear and descriptive names that reflect their purpose, avoiding the `X-` prefix in line with current best practices.
- Ensure custom headers do not conflict with standard HTTP headers and are documented for client and server developers.

Using a consistent approach for custom headers ensures clarity, avoids conflicts with standard headers, and maintains compatibility with legacy systems where necessary.
Tags: `headers` `custom headers` `X- prefix` `legacy systems` `application-specific names`

Let me know if you need any adjustments or additional information!
<br><br>


### ### Always document custom headers clearly to simplify integration and usageEnsure custom headers are well-documented for ease of use and integration

// TODO: add description

```http
// TODO: add example
```

// TODO: complement description

```http
// TODO: add example
```

<br><br>


### Always validate custom header values on both client and server sides to ensure data integrity

// TODO: add description

```http
// TODO: add example
```

// TODO: complement description

```http
// TODO: add example
```

<br><br>


### Prefer concise and descriptive names for custom headers to enhance readability
When defining custom headers, ensure the names are concise yet descriptive to enhance readability and maintainability. This
helps both developers and systems to understand and handle the headers efficiently.

**Examples**
- Client Identification: When adding a custom header for client identification, use a name like `Client-ID` that is brief yet clearly indicates its purpose.
- Request Tracking: When using a custom header for tracking requests, a name like `Request-ID` is short and immediately conveys its function.
- Feature Flags: When including feature flags or toggles, a name like `Feature-Flag` is both succinct and explanatory.

To implement concise yet descriptive custom headers:
- Choose names that are as short as possible while still clearly indicating the header�s purpose.
- Avoid unnecessary abbreviations that could obscure the header�s meaning.
- Ensure the header names are consistent across different parts of the application for uniformity.

Tags: `headers` `custom headers` `concise` `descriptive` `readability`
<br><br>


### Use custom headers to convey metadata that does not fit within the standard headers

// TODO: add description

```http
// TODO: add example
```

// TODO: complement description

```http
// TODO: add example
```

<br><br>


### Avoid exposing sensitive information in custom headers to enhance security
Custom headers should never contain sensitive information, such as API keys, authentication tokens, or personally
identifiable information (PII). Exposing this data in headers increases the risk of security vulnerabilities, as
headers can be intercepted or logged unintentionally. Instead, sensitive information should be handled securely
through other mechanisms, such as encryption or secure token-based authentication.

**Best Practices:**
- **Use secure tokens**: Securely store tokens (e.g., JWTs) and avoid sending raw sensitive data.
- **Minimize data exposure**: Only send the information absolutely necessary for the operation.
- **Encrypt data**: Use HTTPS to encrypt header content in transit, especially for sensitive details.

**Example of an insecure custom header:**
```http
GET /api/orders HTTP/1.1
Host: example.com
X-User-Password: myplaintextpassword
```

**Improved version:**
```http
GET /api/orders HTTP/1.1
Host: example.com
Authorization: Bearer <secure_token>
```

In this improved example, the custom header no longer exposes sensitive data. Instead, a secure token
is used for authentication, ensuring better protection against interception.

See also: Security
<br><br>


### Ensure custom headers comply with security protocols, such as encryption when necessary

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


### Leverage custom headers for request tracing and logging to improve debugging capabilities

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


### Implement custom header support in a backward-compatible manner
It is important to ensure backward compatibility, when adding custom headers, to avoid breaking existing clients. Custom headers
should be optional and their absence should not affect the functionality of the API for clients that do not support them. This ensures
a smooth transition when introducing new features or improvements, while still maintaining support for older versions of clients.

**Best Practices:**
- **Gracefully handle missing headers**: Ensure that the API functions correctly even when custom headers are not present.
- **Document custom headers**: Clearly document the custom headers and how they can enhance API functionality without making them mandatory.
- **Version the API carefully**: If necessary, use API versioning when introducing new custom headers, but ensure clients not sending those headers still receive valid responses.

**Example of backward-compatible custom header usage:**

Without the custom header:
```http
GET /api/products HTTP/1.1
Host: example.com
```

With the custom header (optional):
```http
GET /api/products HTTP/1.1
Host: example.com
X-Custom-Filter: featured
```

In this example, the API works without the `X-Custom-Filter` header, but clients can choose to use it for enhanced functionality (e.g.,
filtering for featured products) without breaking compatibility.

See also: compatibility
<br><br>


### Minimize performance overhead by optimizing the processing of custom headers

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


### Handle errors gracefully when custom headers are missing or malformed
When designing APIs that rely on custom headers, it's important to handle errors gracefully if those headers are missing
or malformed. Instead of failing unexpectedly, the API should provide meaningful error messages or default behavior to help
clients understand what went wrong and how to fix it. Avoid terminating requests abruptly or returning generic error
messages that lack context.

**Best Practices:**
- **Return clear error messages**: When a custom header is required but missing or malformed, respond with a detailed message that describes the problem and how the client can correct it.
- **Use appropriate status codes**: Use HTTP status codes like `400 Bad Request` for malformed headers and `412 Precondition Failed` if a required header is absent.
- **Fallback to defaults**: If possible, use a fallback behavior when a custom header is missing, ensuring the API continues functioning without crashing.

**Example of handling missing or malformed custom headers:**

Missing custom header:
```http
HTTP/1.1 412 Precondition Failed
Content-Type: application/json

{
  "error": "Missing required custom header: X-Custom-Auth. Please provide the header for authentication."
}
```

Malformed custom header:
```http
HTTP/1.1 400 Bad Request
Content-Type: application/json

{
  "error": "Invalid value for custom header: X-Custom-Filter. Expected format: [keyword], got: [123]."
}
```

In this example, the server gracefully handles errors by providing clear messages about the issues with the custom headers and offering guidance to correct the request.

See also: `error handling`
<br><br>


### Follow industry standards and best practices for naming and using custom headers to enhance interoperability

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