# Performance

<br>


## General
<br>


### Applications should be designed and implemented to reduce bandwidth requirements and improve responsiveness.

// TODO: add description.

```http
// TODO: add example
```

<br><br>


### Applications should support pagination to limit access to large collections of data items, thus reducing network traffic.
Applications should support pagination when returning large collections of data to clients in order to enhance performance,
reduce latency, and manage resource utilization effectively.

**Request:**
```http
GET /api/users?page=2&page_size=10 HTTP/1.1
Host: example.com
```

**Response:**
```json
HTTP/1.1 200 OK
Content-Type: application/json

{
  "total_items": 95,
  "current_page": 2,
  "total_pages": 10,
  "next_page": "http://example.com/api/users?page=3&page_size=10",
  "prev_page": "http://example.com/api/users?page=1&page_size=10",
  "first_page": "http://example.com/api/users?page=1&page_size=10",
  "last_page": "http://example.com/api/users?page=10&page_size=10",
  "users": [
    {
      "id": 11,
      "name": "John Doe"
    },
    {
      "id": 12,
      "name": "Jane Smith"
    },
    ...
  ]
}
```

Pagination helps in the following ways:
- **Performance Optimization**: Reduces the amount of data transferred over the network, thereby improving response times.
- **Resource Management**: Limits the strain on server resources by fetching and processing data in smaller batches.
- **Improved User Experience**: Enables clients to navigate through large datasets efficiently.

<sub>See also: Pagination</sub>
<br><br>



## Compression
<br>


### Considering compressing the payload of response messages before sent back to the client.

As a general guideline, compress the payload of response messages with gzip, unless there are requirements not to do it.

// TODO: complement description.

```http
// TODO: add example
```

<br><br>


### Do not use compression if the amount of requests being served is so high that compression time becomes a bottleneck.

// TODO: add description.

```http
// TODO: add example
```

<br><br>


### Consider supporting both compressed and uncompressed payloads even when using compression by default
When servers use compression by default to reduce payload size and improve performance, they should still support handling requests and
responses without compression. This ensures compatibility with clients that may not support or prefer compression, providing a more robust
and flexible API.

**Example Request for Compressed Payload**
```http
GET /api/products
Accept-Encoding: gzip
```

**Example Response with Compressed Payload**
```http
HTTP/1.1 200 OK
Content-Type: application/json
Content-Encoding: gzip

{compressed data}
```

**Example Request for Uncompressed Payload**
```http
GET /api/products
Accept-Encoding: identity
```

**Example Response with Uncompressed Payload**
```http
HTTP/1.1 200 OK
Content-Type: application/json

{
  "id": 1,
  "name": "Product 1",
  "price": 10.99
  ...
}
```

**Scenarios**
- **Client Incompatibility**: When a client does not support compressed responses and needs uncompressed data.
- **Debugging and Testing**: When developers need to debug or test responses without dealing with compression.
- **Network Conditions**: When network conditions or client preferences dictate the use of uncompressed data for faster processing.

**Benefits**
- **Flexibility**: Supports a wider range of clients with different capabilities and preferences.
- **Compatibility**: Ensures that all clients, including those that do not support compression, can interact with the API.
- **Ease of Use**: Simplifies debugging and testing by allowing responses without compression.

By supporting both compressed and uncompressed payloads, APIs become more versatile and accessible, accommodating the needs and preferences of various clients and improving overall compatibility.

**Tags:** `compression` `compatibility` `flexibility` `payload`
<br><br>


### A server should indicate it is using gzip compression via the `Content-Encoding` header.
Servers should indicate the usage of gzip compression for response payloads by including the `Content-Encoding` header
in HTTP responses. Gzip compression reduces the size of transmitted data, leading to improved network performance and
reduced bandwidth consumption.

**Request:**
```http
GET /api/data HTTP/1.1
Host: example.com
Accept-Encoding: gzip
```

**Response:**
```http
HTTP/1.1 200 OK
Content-Type: application/json
Content-Encoding: gzip

<gzip-compressed-data>
```

<br><br>

