# Message Content
 Message Content refers to the data included in the body of an HTTP request or response. This content conveys the actual
 information being transferred between the client and the server.



## Data Structure
<br>

### Always maintain consistent data structures across endpoints to ensure predictable responses
Maintaining consistent data structures across all endpoints enhances the predictability of API responses, making it
easier for clients to consume data reliably. This consistency reduces parsing errors, simplifies client code, and
ensures that similar resources or entities follow the same structure regardless of the endpoint.

**Guideline**
- Use the same field names, data types, and nesting structures across endpoints when representing similar data.
- Avoid introducing different field names or formats for the same entity type, even if used in different contexts.

**Client Requests**

```http
GET /api/products/123
```

```http
GET /api/orders/456
```

**Server Responses**

```http
HTTP/1.1 200 OK
Content-Type: application/json

// Product Response
{
  "id": 123,
  "name": "Product A",
  "price": 29.99,
  "availability": "In Stock"
}
```

```http
HTTP/1.1 200 OK
Content-Type: application/json

// Order Response with consistent structure for product info
{
  "id": 456,
  "status": "Shipped",
  "products": [
    {
      "id": 123,
      "name": "Product A",
      "price": 29.99,
      "quantity": 1
    }
  ]
}
```

**Scenarios**
- **Unified Entity Representation:** Ensures that, for example, a `product` object is identical across different endpoints (e.g., product listings and order details).
- **Improved Client Parsing:** Reduces the need for custom parsing logic, as clients can reuse code for similar data structures.
- **Reduced Errors:** Consistency in naming and formatting minimizes confusion and errors when integrating new endpoints or features.

Tags: data structure consistency, response predictability, API design
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

Tags: `Content Negotiation` `Accept Header` `Response Format` `HTTP Headers` `Flexible Responses` `Client Preferences`
<br><br>


### Consider optimizing the size of the payload by excluding unnecessary data and using efficient data formats
Minimizing payload size improves API performance by reducing bandwidth usage and response times. This can be achieved
by excluding redundant or unnecessary data fields and using efficient data formats like JSON or gzip compression. Smaller
payloads also benefit mobile or low-bandwidth clients.

- **Selective Fields:** Allow clients to request specific fields using query parameters (e.g., `fields` or `select`).  
- **Efficient Formats:** Use compressed data formats (e.g., gzip) or lean formats (e.g., JSON) for serialization or optimise structures for frequently accessed large datasets.
- **Remove Redundancy:** Exclude verbose metadata, unused fields, or unnecessary nested structures.

**Client Request**

```http
GET /api/products/123?fields=id,name,price
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

**Scenarios**
- **Reduced Fields:** An API for listing products excludes full descriptions and reviews by default, only adding them when explicitly requested.  
- **Paginated Results:** Truncate responses to manageable sizes for paginated endpoints.  
- **Batch Compression:** Compress large datasets (e.g., logs or analytics) for efficient transmission.  

**Tags**: payload optimization, data formats, efficient APIs, performance improvement
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


### Always use JSON as the payload data interchange format

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


### Object names should be singular
When defining objects in JSON data or message content, using singular names ensures clarity and
consistency. Singular naming reinforces the concept that each object represents a single instance
or entity, making the structure easier to understand and work with.

- **Singular Naming for Object Keys**: Use singular names for JSON object keys to reflect individual entities.  
- **Avoid Plural Keys for Single Entities**: Plural naming may suggest collections, leading to confusion.  
- **Consistency in Data Structures**: Apply this rule uniformly across all responses and request payloads.  

**Example**

**Correct: Singular Object Names**

```json
{
  "user": {
    "id": 123,
    "name": "Alice",
    "email": "alice@example.com"
  },
  "order": {
    "id": 456,
    "total": 99.99
  }
}
```

**Incorrect: Plural Object Names for Single Entities**

```json
{
  "users": {
    "id": 123,
    "name": "Alice",
    "email": "alice@example.com"
  },
  "orders": {
    "id": 456,
    "total": 99.99
  }
}
```

**Scenarios**  
- **Nested Data Structures**: Singular object names are particularly important in nested data to avoid ambiguity.  
- **Interoperability**: Consistent naming conventions make it easier for clients to understand and use the API.  

**Cautions**  
- **Collections of Objects**: Use plural names only when the object explicitly represents a collection (e.g., an array of resources). For example, `users` could refer to a list of user objects.  

By using singular names for JSON objects, you ensure the API content remains clear, intuitive, and aligned with best practices for data representation.

**Tags**: JSON structure, naming conventions, singular, message consistency, data clarity
<br><br>


### Do not use `null` for boolean properties
In JSON message content, avoid using `null` as a value for boolean properties. Booleans should represent
definitive `true` or `false` states, ensuring clarity and reducing ambiguity for clients consuming the API.

- **Clarity of Meaning**: Boolean properties inherently represent binary states and should not include a third "unknown" or `null` value.  
- **Use Enums for Ambiguity**: If a property can have more than two states, such as "true," "false," and "unknown," replace the boolean with an enumeration for better readability and flexibility.  
- **Default Values**: Use explicit `true` or `false` values instead of `null` when the state is known or defaultable.  

**Examples**

**Incorrect**: Using `null` for a boolean property  
```json
{
  "isAvailable": null
}
```

**Correct**: Using explicit boolean values  
```json
{
  "isAvailable": false
}
```

**Alternative**: Using an enumeration for multiple states  
```json
{
  "availabilityStatus": "unknown"  // "available", "unavailable", or "unknown"
}
```

**Scenarios**  
- **Ambiguous States**: Replacing `null` booleans with enums ensures clarity when a state cannot be determined.  
- **Default Values**: When a boolean can default to `false` (e.g., "isActive"), avoid `null`.  

**Cautions**  
- **Parsing Issues**: Some JSON parsers or consumers may misinterpret `null` for booleans, causing unexpected errors.  
- **Validation Complexity**: Avoiding `null` simplifies validation logic for both the server and client.  

**Tags**: JSON message content, boolean properties, null values, enumerations.
<br><br>


### Prefer the use of enumerations of named values instead of nullable boolean properties
Using enumerations of named values in JSON message content or data structures enhances clarity and expressiveness
compared to nullable boolean properties. Enumerations provide a clearer context for potential states, reducing
ambiguity and improving the readability and maintainability of the API.

- **Enumerations Over Nullable Booleans**: Replace nullable boolean properties with enumerations to represent all possible states explicitly.  
- **Clarity in States**: Enumerations avoid confusion over the meaning of `null` or missing values.  
- **Expandability**: Enumerations are easier to extend when new states are needed.  

**Example**

**Preferred: Enumeration of Named Values**

```json
{
  "order": {
    "id": 123,
    "status": "pending" 
  }
}
```

Here, `status` uses an enumeration (`"pending"`, `"shipped"`, `"delivered"`) to represent the state of the order.

**Avoid: Nullable Boolean**

```json
{
  "order": {
    "id": 123,
    "isPending": true,
    "isShipped": null,
    "isDelivered": null
  }
}
```

Nullable boolean values are harder to interpret, especially when multiple related flags exist.

**Scenarios**  
- **State Representation**: For fields representing a resource's state or condition, enumerations convey meaning more effectively than booleans.  
- **Validation and Documentation**: Enumerations allow for well-defined, restricted sets of values, making validation simpler and documentation clearer.  

**Cautions**  
- **Overly Broad Enumerations**: Ensure enumerations are concise and meaningful; overly broad sets can introduce complexity.  
- **Backward Compatibility**: When extending enumerations with new values, maintain backward compatibility with existing clients.  

By adopting enumerations for named values, APIs become more intuitive and robust, reducing potential misunderstandings and simplifying integration for clients.

**Tags**: JSON design, enumerations, boolean properties, state representation, API clarity.
<br><br>


### Array names should be pluralized
When representing arrays in JSON message content, ensure the property names are pluralized. This practice enhances
readability and clarity by accurately reflecting the data structure as a collection of multiple items.  

- **Pluralize Array Property Names**: Use plural nouns to describe properties containing arrays, indicating that the data represents a collection.  
- **Avoid Ambiguity**: Singular names can cause confusion, as they may imply a single object rather than a list.  

**Examples**  

1. **Correct Usage**  
```json
{
  "products": [
    { "id": 1, "name": "Laptop" },
    { "id": 2, "name": "Phone" }
  ]
}
```

2. **Incorrect Usage**  
```json
{
  "product": [
    { "id": 1, "name": "Laptop" },
    { "id": 2, "name": "Phone" }
  ]
}
```

**Scenarios**  
- **Resource Collections**: Use pluralized names for endpoints returning multiple items, such as `users`, `orders`, or `products`.  
- **Nested Arrays**: Apply the same principle to nested properties within a larger JSON structure.  

**Benefits**  
- **Improved Readability**: Clearly communicates that the property represents a collection.  
- **Consistency**: Ensures uniformity across API responses and aligns with common best practices.  
- **Ease of Parsing**: Helps client developers anticipate and handle arrays correctly.  

**Cautions**  
- **Avoid Unnecessary Pluralization**: Only pluralize properties that are explicitly arrays. Do not pluralize singular objects or other data types.  
- **Maintain Consistency**: Ensure pluralized naming conventions are applied consistently across all endpoints and responses.  

**Tags**: json conventions, array naming, message structure, api design.  
<br><br>


### Prefer the use of the empty list representation instead of `null` for empty arrays
When representing empty collections in JSON data, always use an empty array (`[]`) rather than `null`. This approach
promotes consistency and avoids ambiguity in the interpretation of the data.  

- **Use `[]` for Empty Arrays**: Ensure that any field representing a collection defaults to an empty array if no data is present, instead of assigning `null`.  
- **Avoid Ambiguity**: Using `null` can imply that the field is missing or undefined, leading to potential misinterpretation by clients.  
- **Consistent Type Handling**: Clients consuming the API can always expect an array, simplifying client-side validation and processing.  

**Examples**  

1. **Correct Representation**  
```json
{
  "items": []
}
```  

2. **Incorrect Representation**  
```json
{
  "items": null
}
```  

**Scenarios**  
- **No Data Available**: When a query returns no results, such as a user with no associated orders or a product with no reviews, use an empty array to represent the absence of data.  
- **Predefined Collections**: For API responses that always include specific fields representing collections, default to an empty array when the collection has no elements.  

**Benefits**  
- **Simplified Client Logic**: Clients can uniformly treat all array fields as iterable, even when they are empty, reducing error handling.  
- **Avoids Misinterpretation**: Differentiates between "no items available" (`[]`) and "field is missing or undefined" (`null`).  

**Cautions**  
- **Schema Validation**: Ensure that your API's data schema explicitly defines array types to enforce consistent behavior.  
- **Backward Compatibility**: If existing APIs use `null` for empty arrays, transitioning to empty arrays may require careful coordination to avoid breaking changes.  

**Tags**: json consistency, empty collections, null values, api response formatting.  
<br><br>


### Do not perform date localization in the API
APIs should avoid localizing dates and times. Instead, they should provide standardized formats (e.g., ISO 8601)
and let client applications handle localization based on the user's context. This approach ensures consistency,
simplifies server-side logic, and supports a broader range of client-side customizations.  

- **Standardized Format**: Always return dates and times in a universally recognized format, such as ISO 8601 (e.g., `2024-12-01T12:00:00Z` for UTC).  
- **Client Responsibility**: Allow client applications to format and localize dates based on user preferences, time zones, or regional settings.  
- **Avoid Ambiguity**: Do not include localized date strings or region-specific formats in API responses.  

**Examples**  

**Incorrect**: Localizing dates on the server  
```json
{
  "eventDate": "01-Dec-2024, 12:00 PM IST" // Locale-specific format
}
```  

**Correct**: Returning standardized date formats  
```json
{
  "eventDate": "2024-12-01T12:00:00Z" // ISO 8601 in UTC
}
```  

**Scenarios**  
- **Global Applications**: APIs serving clients in multiple regions should avoid server-side localization to prevent inconsistencies.  
- **User-Specific Localization**: Clients can format the date appropriately for their user's language or time zone (e.g., using libraries like `Intl.DateTimeFormat` in JavaScript).  

**Cautions**  
- **Parsing Errors**: Localized strings can cause parsing issues in client applications due to differences in regional formats.  
- **Time Zone Handling**: Clearly indicate whether the date is in UTC or a specific time zone to avoid misinterpretations.  

**Tags**: JSON message content, date localization, ISO 8601, time zone handling.  
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


