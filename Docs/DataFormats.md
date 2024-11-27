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


## Clearly Specify the Response Format Using Content-Type Headers

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

## Document Supported Data Formats for Each Endpoint

## Validate Input Data Against a Schema (e.g., JSON Schema)

## Support Data Compression for Large Payloads (e.g., gzip)