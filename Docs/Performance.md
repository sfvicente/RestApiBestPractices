# Performance
This section focuses on optimizing the efficiency and responsiveness of APIs. It covers best practices such as minimizing payload size,
supporting pagination, compressing responses, and reducing bandwidth usage. By implementing these strategies, APIs can handle large datasets
and high traffic loads more effectively, providing faster, more scalable, and resource-efficient services to clients.
<br>


## General Guidelines
<br>


### Always design applications to minimize bandwidth usage and enhance responsiveness

// TODO: add description.

```http
// TODO: add example
```

<br><br>


### Always implement pagination to efficiently manage large data collections and minimize network traffic
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

Tags: `Pagination` `Data Collection Management` `Performance Optimization` `Resource Efficiency` `Network Traffic` `User Experience` `Response Structure`
<br><br>



## Compression Guidelines
<br>


### Consider compressing response payloads before sending them to the client

As a general guideline, compress the payload of response messages with gzip, unless there are requirements not to do it.

// TODO: complement description.

```http
// TODO: add example
```

<br><br>


### Avoid using compression when high request volume causes performance bottlenecks
Compression can reduce the size of response payloads, improving bandwidth usage and reducing transmission time. However, in high-traffic
environments where the number of requests is extremely high, the time spent compressing data can become a performance bottleneck. In such
cases, the cost of compressing responses may outweigh the benefits of reduced payload size, leading to increased latency and reduced server
throughput.

If the server's CPU resources are constrained or the overhead of compression significantly delays response times, it may be better to serve
uncompressed data to ensure faster processing and response delivery.

**Considerations:**
- **CPU Overhead**: Compression requires processing power. In high-load scenarios, this could lead to resource exhaustion.
- **Latency**: The time spent compressing data may increase the total response time, especially for smaller payloads that don't benefit much from compression.
- **Server Load**: When request volume is high, prioritizing fast response times over compression can help maintain system performance.

**Alternatives:**
- **Selective Compression**: Compress only large payloads where the compression benefits are more substantial, while avoiding compression for small responses.
- **Offloading Compression**: Use dedicated hardware or proxies for compression if compression is required and request volume is high.

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


### Always indicate gzip compression using the `Content-Encoding` header
Servers should indicate the usage of gzip compression for response payloads by including the `Content-Encoding` header in HTTP
responses. Gzip compression reduces the size of transmitted data, leading to improved network performance and reduced bandwidth
consumption. This header informs clients that the response is compressed, allowing them to properly decompress the data.

**Example Request**
```http
GET /api/data HTTP/1.1
Host: example.com
Accept-Encoding: gzip
```

**Example Response**
```http
HTTP/1.1 200 OK
Content-Type: application/json
Content-Encoding: gzip

<gzip-compressed-data>
```

**Scenarios**
- **Large Data Sets**: When serving large datasets or files, gzip compression can significantly reduce the amount of data transferred.
- **Improved Performance**: In scenarios where network bandwidth is limited or costly, gzip compression helps to minimize data transfer sizes, improving response times.
- **Bandwidth Optimization**: For APIs with high traffic, gzip compression can lead to considerable savings in bandwidth usage.

**Benefits**
- **Efficiency**: Reduces the amount of data that needs to be transmitted, speeding up data transfer and improving response times.
- **Cost Savings**: Lower bandwidth consumption can lead to cost savings, especially for services with high data transfer volumes.
- **Client Compatibility**: Most modern clients and browsers support gzip compression, making it a widely compatible solution for data transfer optimization.

Using the `Content-Encoding` header to indicate gzip compression helps ensure that clients can correctly interpret and decompress the response, maintaining the integrity and usability of the transmitted data.

Tags: `Compression` `Payload Management` `Performance` `Client Compatibility` `Accept-Encoding` `Content-Encoding` `Debugging` `Network Efficiency` `Response Handling`
<br><br>


