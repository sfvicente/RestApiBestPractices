# Data Formats
The **Data Formats** section focuses on standardizing how data is represented and transmitted in APIs to ensure
consistency, efficiency, and interoperability. It includes guidelines on default formats like JSON, efficient
encoding practices, and techniques for minimizing payload size to optimise performance and enhance client compatibility.

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
While JSON is the default and most widely used format for modern REST APIs, there are scenarios where
supporting additional formats like XML may be required. However, these formats should only be implemented
when there is a clear and justified need, such as compliance with legacy systems or specific client requirements.

- **Default to JSON**: Use JSON as the primary data format for API responses.  
- **Add XML Support When Required**: Introduce XML or other formats only if necessary, such as for legacy system compatibility or regulatory compliance.  
- **Use Content Negotiation**: Allow clients to specify their preferred format using the `Accept` header.  
- **Avoid Over-Complexity**: Ensure additional formats do not overcomplicate the API's implementation, documentation, or maintenance.  

**Example of Content Negotiation**

**Client Request for JSON**

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
  "price": 29.99
}
```

**Client Request for XML**

```http
GET /api/products/123
Accept: application/xml
```

**Server Response**

```http
HTTP/1.1 200 OK
Content-Type: application/xml

<product>
  <id>123</id>
  <name>Product A</name>
  <price>29.99</price>
</product>
```

**Scenarios**  
- **Legacy System Support**: When the API must interact with older systems that only support XML.  
- **Regulatory Requirements**: Some industries may mandate the use of XML for data exchange.  
- **Custom Client Needs**: Certain clients may require XML for integration with their systems.  

**Cautions**  
- **Increased Complexity**: Supporting multiple formats may lead to more complex code and increased testing efforts.  
- **Documentation Challenges**: Ensure all supported formats are documented clearly to avoid client confusion.  

Supporting additional formats like XML only when necessary balances modern best practices with practical requirements, ensuring flexibility without sacrificing simplicity.

**Tags**: data formats, JSON, XML, content negotiation, legacy systems, API simplicity
<br><br>


## Always clearly specify the response format using content-type headers
APIs must explicitly indicate the format of the response body by using the `Content-Type` header. This ensures
that clients can correctly interpret the data format, reducing errors and enhancing compatibility between clients and servers.  

- **Set the `Content-Type` Header**: Always include the `Content-Type` header in responses to specify the media type of the response body (e.g., `application/json` for JSON).  
- **Match the Response Body**: Ensure the value of the `Content-Type` header aligns with the actual format of the response payload.  
- **Use Standard Media Types**: Stick to widely accepted MIME types such as `application/json`, `application/xml`, or others appropriate for the API.  

**Examples**  

**Correct**: Explicitly specifying `Content-Type`  
```http
HTTP/1.1 200 OK
Content-Type: application/json

{
  "id": 123,
  "name": "Laptop",
  "price": 999.99
}
```  

**Incorrect**: Missing or mismatched `Content-Type`  
```http
HTTP/1.1 200 OK

{
  "id": 123,
  "name": "Laptop",
  "price": 999.99
}
```  

**Scenarios**  
- **Dynamic Responses**: When an endpoint supports multiple response formats, use `Content-Type` to indicate the specific format returned.  
- **Error Responses**: Include the `Content-Type` header even in error responses to maintain consistency.  

**Cautions**  
- **Omissions**: Missing or incorrect `Content-Type` headers can lead to parsing errors or unexpected client behaviour.  
- **Non-Standard Types**: Avoid using custom MIME types unless absolutely necessary and well-documented.  

**Tags**: content negotiation, content-type, response headers, JSON, XML.  
<br><br>


## Standardize Date and Time Fields Using ISO 8601
Date and time fields in REST APIs should follow the [ISO 8601](https://www.iso.org/iso-8601-date-and-time-format.html)
standard. This format ensures consistency, reduces ambiguity, and promotes interoperability between systems. ISO 8601
provides a universal and unambiguous structure for representing dates and times, supporting both local and UTC formats.

- **Always Use ISO 8601 Format**: Represent dates and times in the `YYYY-MM-DDTHH:mm:ssZ` format (e.g., `2024-12-01T15:30:00Z` for UTC).  
- **Indicate Time Zones**: Include a time zone offset (`+00:00` or `Z` for UTC) to avoid confusion when interpreting timestamps.  
- **Use Consistent Formats Across APIs**: Standardize date and time representations across all endpoints to ensure predictability for clients.

**Client Request**

```http
GET /api/events?start_date=2024-12-01T00:00:00Z&end_date=2024-12-31T23:59:59Z
```

**Server Response**

```http
HTTP/1.1 200 OK
Content-Type: application/json

[
  {
    "id": 1,
    "name": "New Year Celebration",
    "date": "2024-12-31T23:00:00Z"
  },
  {
    "id": 2,
    "name": "Christmas Party",
    "date": "2024-12-25T18:00:00Z"
  }
]
```

**Scenarios**
- **Event Scheduling**: Use ISO 8601 to schedule events with precise start and end times.  
- **Filtering Data**: Allow clients to filter resources based on standardized date and time fields (e.g., `start_date` and `end_date`).  
- **Auditing and Logs**: Store timestamps in ISO 8601 format for consistent auditing and debugging.  

By adopting ISO 8601, APIs eliminate discrepancies caused by varying date formats, simplify internationalisation, and enable seamless
integration with clients and systems worldwide.

**Tags**: ISO 8601, date formatting, time zones, standardization, REST best practices
<br><br>


## Adopt Consistent Naming Conventions for Fields (e.g., camelCase or snake_case)

## Minimize Payload Size by Avoiding Unnecessary Fields

## Use Arrays or Objects Consistently for Collections
When representing collections in your API responses, maintain consistency by choosing either arrays
or objects to structure the data. This ensures predictable responses and reduces client-side complexity
when processing collections.

Inconsistent use of arrays and objects can confuse clients and complicate the deserialization process. A
uniform approach enables better usability and prevents ambiguity in the data structure.

**Inconsistent representation**
```json
// Object for a single item
{
  "user": {
    "id": 1,
    "name": "John Doe"
  }
}

// Array for multiple items
{
  "users": [
    { "id": 1, "name": "John Doe" },
    { "id": 2, "name": "Jane Doe" }
  ]
}
```

**Consistent representation (using arrays for collections)**
```json
{
  "users": [
    { "id": 1, "name": "John Doe" },
    { "id": 2, "name": "Jane Doe" }
  ]
}
```

**Consistent representation (using objects for collections)**
```json
{
  "users": {
    "1": { "name": "John Doe" },
    "2": { "name": "Jane Doe" }
  }
}
```

**Recommendations**
- Use arrays when the collection has no inherent key-value relationships and order is important.
- Use objects when each item in the collection can be uniquely identified by a key, such as an ID.
- Clearly document the chosen format in your API specification to avoid client-side confusion.
<br><br>


## Document Supported Data Formats for Each Endpoint
Clearly documenting the supported data formats for each endpoint ensures that API consumers understand
how to send requests and interpret responses. This transparency reduces implementation errors, improves
developer experience, and promotes interoperability.  

**Guideline**  
- **List Supported Formats in API Documentation**: Include all acceptable request and response formats for each endpoint, such as JSON, XML, or others.  
- **Specify Default Formats**: Clearly indicate the default format if none is explicitly requested by the client.  
- **Provide Content Negotiation Details**: Explain how clients can request specific formats using headers like `Accept` or `Content-Type`.  

**Examples**  

1. **API Documentation Snippet**  
```plaintext
Endpoint: GET /users  
Supported Formats:  
- Request: JSON (`application/json`)  
- Response: JSON (`application/json`)  
Default Format: JSON  
To request an XML response, include the header `Accept: application/xml`.
```  

2. **Header Example for Requesting Formats**  
```http
GET /users HTTP/1.1  
Host: api.example.com  
Accept: application/json  
```

**Scenarios**  
- **Multi-Format Support**: If the API supports multiple formats, document which endpoints accept or return specific formats.  
- **Backward Compatibility**: Clearly outline how older clients using deprecated formats will be handled.  

**Benefits**  
- **Transparency**: Reduces ambiguity and sets clear expectations for API consumers.  
- **Error Reduction**: Minimizes issues caused by unsupported or incorrectly formatted requests.  
- **Improved Developer Experience**: Makes it easier for developers to integrate and test API interactions.  

**Cautions**  
- **Format Proliferation**: Avoid supporting too many formats unless necessary, as this can complicate maintenance.  
- **Documentation Accuracy**: Keep documentation up to date as formats evolve or change.  

**Tags**: api documentation, content negotiation, data formats, supported formats, developer experience.  
<br><br>


## Validate Input Data Against a Schema (e.g., JSON Schema)
Input validation ensures that incoming data adheres to expected formats, types, and constraints. By using
schemas such as JSON Schema, APIs can systematically enforce these rules, reducing the risk of invalid data
corrupting systems or causing errors.

- Validating input data improves API reliability by ensuring only well-formed requests are processed.
- Schema-based validation provides a standardised, reusable way to handle input constraints, simplifying development and maintenance.
- Preventing invalid data at the boundary reduces the likelihood of internal failures or security vulnerabilities like injection attacks.

**Sample JSON schema**
```json
{
  "$schema": "https://json-schema.org/draft/2020-12/schema",
  "type": "object",
  "properties": {
    "username": {
      "type": "string",
      "minLength": 3
    },
    "email": {
      "type": "string",
      "format": "email"
    },
    "age": {
      "type": "integer",
      "minimum": 0
    }
  },
  "required": ["username", "email", "age"],
  "additionalProperties": false
}
```

**Example Request Using Schema Validation**

**Request Body**
```json
{
  "username": "JohnDoe",
  "email": "john.doe@example.com",
  "age": 25
}
```

**Validation Result**
- Passes validation: all required fields are present and meet the defined constraints.

**Invalid Request Body**
```json
{
  "username": "JD",
  "email": "not-an-email"
}
```

**Validation Errors**
- `username` fails `minLength` validation.
- `email` fails `format` validation.

**HTTP Response**
```http
HTTP/1.1 400 Bad Request
Content-Type: application/json

{
  "errors": [
    { "field": "username", "message": "Must be at least 3 characters long." },
    { "field": "email", "message": "Must be a valid email address." }
  ]
}
```

**Implementation considerations**
- Use robust schema validation libraries (e.g., AJV for JSON Schema) for server-side validation.
- Provide meaningful error messages to guide clients in correcting their requests.
- Extend schemas to handle dynamic requirements or complex nested structures when necessary.
- Validate against schemas both during development (e.g., unit tests) and runtime.

Schema validation should always be applied to any API endpoint that accepts structured data. It is especially important
for endpoints handling user-generated input or integrations with external systems.
<br><br>

## Support Data Compression for Large Payloads (e.g., gzip)