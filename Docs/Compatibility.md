# Compatibility


## General Guidelines
<br>


### Avoid ignoring unknown input fields in the message payload by returning an error with an HTTP 400 status code
To maintain strict validation and ensure the integrity of API requests, avoid silently ignoring unknown input fields in the message
payload. Instead, return a clear error response, such as an HTTP `400 Bad Request` status code, to inform clients that the request
includes invalid or unexpected data. This approach prevents confusion, ensures clients are aware of any incorrect usage, and reinforces
proper use of the API.

By validating payloads and rejecting requests with unknown fields, you can reduce potential security risks, prevent data pollution,
and make the API behavior more predictable and reliable. Clear feedback also helps developers quickly identify mistakes and adjust
their client requests accordingly.

**Key Points:**
- **Enhances clarity and transparency**: Clients are informed of mistakes rather than unknowingly submitting invalid data.
- **Improves security**: Rejecting unknown fields reduces the attack surface by avoiding unanticipated inputs.
- **Reinforces proper API usage**: Ensures clients adhere to the API’s expected schema and structure.

**Example of an invalid request with unknown fields:**
```http
POST /api/v1/users
Content-Type: application/json

{
  "name": "John Doe",
  "email": "john.doe@example.com",
  "age": 30,  // Valid field
  "unexpectedField": "some value"  // Unknown field
}
```

**Response:**
```http
HTTP/1.1 400 Bad Request
Content-Type: application/json

{
  "error": "Unknown field: unexpectedField"
}
```

In this example, the API rejects the request and returns an error message indicating that an unknown field was provided.

Additional Tags: Payload, HTTP 400
<br><br>


### Avoid ignoring unknown input fields in the URI by returning an error with an HTTP 400 status code.

// TODO: add description

```http
// TODO: add example
```

// TODO: complement description

```http
// TODO: add example
```

Additional Tags: URIs, HTTP 400
<br><br>



## ...