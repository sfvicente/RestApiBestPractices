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


### Even when using compression by default, servers should also support payload without compression.

// TODO: add description.

```http
// TODO: add example
```

<br><br>


### A server should indicate it is using gzip compression via the `Content-Encoding` header.

// TODO: add description.

```http
// TODO: add example
```

<br><br>

