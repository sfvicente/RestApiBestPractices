# Data Formats


## General

...


## ...

## Use JSON as the Default Data Format for Responses
JSON is widely supported, lightweight, and easy to read, making it the preferred data format for REST API
responses. Using JSON as the default ensures compatibility with most modern programming languages and
tools, streamlining client integration and simplifying data processing.

- Always return API responses in JSON format unless explicitly requested otherwise by the client (e.g., via `Accept` headers).  
- Adhere to a consistent JSON structure with clear keys, appropriate nesting, and predictable data types.  
- Include a `Content-Type: application/json` header in all responses to indicate the format.

**Client Request**

```http
GET /api/products/123
Accept: application/json
```

**Server Response**

```http
HTTP/1.1 200 OK
Content-Type: application/json

{
  "id": 123,
  "name": "Product A",
  "price": 29.99,
  "availability": "In Stock"
}
```

**Scenarios**
- **Default Format:** JSON is returned for standard requests without additional headers.  
- **Error Handling:** Ensure error responses (e.g., `400 Bad Request`) are also in JSON format for consistency.  
- **Interoperability:** JSON ensures seamless data exchange with web applications, mobile apps, and other services.

JSON's simplicity and ubiquity make it an ideal default data format for REST APIs, ensuring broad compatibility and ease of use.

**Tags**: JSON, default format, content negotiation, REST best practices
<br><br>


## Support Additional Formats like XML Only When Necessary

## Clearly Specify the Response Format Using Content-Type Headers

## Standardize Date and Time Fields Using ISO 8601

## Adopt Consistent Naming Conventions for Fields (e.g., camelCase or snake_case)

## Minimize Payload Size by Avoiding Unnecessary Fields

## Use Arrays or Objects Consistently for Collections

## Document Supported Data Formats for Each Endpoint

## Validate Input Data Against a Schema (e.g., JSON Schema)

## Support Data Compression for Large Payloads (e.g., gzip)