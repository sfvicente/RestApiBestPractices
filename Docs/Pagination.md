# Pagination
Pagination is a technique used in REST APIs for managing large datasets efficiently. It allows clients to request data in
smaller, manageable chunks using query parameters, improving performance and user experience.

## General
<br>


### Consider supporting partial sets on service operations that return collections
When designing API endpoints that return collections of resources, consider supporting partial sets to improve performance and
efficiency. This involves implementing pagination, filtering, and sorting mechanisms to allow clients to request and process
manageable chunks of data.

**Client Request for Pagination**
```http
GET /api/products?page=2&limit=10
```

**Server Response**
```http
HTTP/1.1 200 OK
Content-Type: application/json

{
  "page": 2,
  "limit": 10,
  "totalItems": 50,
  "totalPages": 5,
  "items": [
    { "id": 11, "name": "Product 11", "price": 10.99 },
    { "id": 12, "name": "Product 12", "price": 12.99 },
    ...
    { "id": 20, "name": "Product 20", "price": 20.99 }
  ]
}
```

**Client Request for Filtering**
```http
GET /api/products?category=electronics&price[lt]=100
```

**Server Response**
```http
HTTP/1.1 200 OK
Content-Type: application/json

{
  "page": 1,
  "limit": 10,
  "totalItems": 25,
  "totalPages": 3,
  "items": [
    { "id": 1, "name": "Product 1", "price": 99.99, "category": "electronics" },
    { "id": 2, "name": "Product 2", "price": 89.99, "category": "electronics" },
    ...
    { "id": 10, "name": "Product 10", "price": 79.99, "category": "electronics" }
  ]
}
```

**Client Request for Sorting**
```http
GET /api/products?sort=price&order=asc
```

**Server Response**
```http
HTTP/1.1 200 OK
Content-Type: application/json

{
  "page": 1,
  "limit": 10,
  "totalItems": 50,
  "totalPages": 5,
  "items": [
    { "id": 21, "name": "Product 21", "price": 5.99 },
    { "id": 22, "name": "Product 22", "price": 6.99 },
    ...
    { "id": 30, "name": "Product 30", "price": 14.99 }
  ]
}
```

**Scenarios**
- Large Collections: When the collection of resources is large, supporting partial sets through pagination prevents overwhelming the client and the server.
- Specific Data Requests: When clients need specific subsets of data based on criteria, filtering allows them to retrieve only the relevant resources.
- Ordered Data Retrieval: When clients need data in a specific order, sorting mechanisms help them receive the data in the desired sequence.

To implement partial sets effectively:
- Use query parameters such as `page`, `limit`, `sort`, `order`, and filter criteria to handle requests for partial sets.
- Return metadata in the response to inform the client about the total number of items, pages, and the current page.
- Ensure that the API documentation clearly explains how clients can use these query parameters to request partial sets.

Supporting partial sets on service operations enhances performance, reduces load on the server, and provides a better user experience by
allowing clients to retrieve and process data efficiently.

Tags: `pagination` `filtering` `sorting` `partial sets` `collections` `performance`
<br><br>


### Clients of service operations that support partial sets must expect limited result sets of information
Clients interacting with service operations that support partial sets must be prepared to handle responses containing 
limited subsets of the full dataset. This means clients should anticipate and correctly process partial results rather
than assuming they have received the entire dataset.

**Example Request**
```http
GET /api/products?page=1&limit=10
```

**Example Response**
```http
HTTP/1.1 200 OK
Content-Type: application/json

{
  "totalItems": 50,
  "totalPages": 5,
  "currentPage": 1,
  "itemsPerPage": 10,
  "products": [
    { "id": 1, "name": "Product 1", "price": 10.0 },
    { "id": 2, "name": "Product 2", "price": 12.5 },
    // ...additional products...
    { "id": 10, "name": "Product 10", "price": 15.0 }
  ]
}
```

**Scenarios**
- **Pagination**: When the service returns paginated data, clients must handle partial datasets and use pagination parameters to retrieve additional data as needed.
- **Large Datasets**: For services dealing with large datasets, clients should expect to receive a limited number of items per response and handle multiple requests to fetch the complete dataset.
- **Performance Optimization**: When services limit the amount of data returned to improve performance, clients should be prepared to request further data in a controlled manner.

**Benefits**
- **Efficient Data Handling**: Ensures clients manage large datasets efficiently by processing and requesting data in smaller chunks.
- **Improved Performance**: Helps maintain optimal performance and reduce server load by limiting the amount of data processed and transferred in each request.
- **Clear Communication**: Provides clients with clear information about the dataset limits and the need to handle partial results, promoting better client-server interaction.

Tags: `partial sets` `pagination` `limited results` `client expectations` `data handling` `performance optimization`
<br><br>


### Clients of service operations that support partial sets are expected to correctly use pagination to retrieve the entire collection

// TODO: add description

```http
// TODO: add example
```

// TODO: complement description

```http
// TODO: add example
```

<br><br>



## ...


### Always use query parameters for pagination
Utilize standard query parameters like `page` and `limit` to allow clients to specify which page of results they want and how many
items per page. Using query parameters for pagination is preferred because it provides a clear, standardized, and intuitive way for clients to navigate
large datasets. This method allows for easy specification of pages and limits, facilitating consistent and predictable access to
data. Additionally, query parameters are part of the URL, making them easily accessible and modifiable, which enhances the user experience
and simplifies implementation and debugging.

**Client Request**
```http
GET /api/products?page=2&limit=10
```

**Server Response**
```http
HTTP/1.1 200 OK
Content-Type: application/json

{
  "page": 2,
  "limit": 10,
  "totalItems": 50,
  "totalPages": 5,
  "items": [
    { "id": 11, "name": "Product 11", "price": 10.99 },
    { "id": 12, "name": "Product 12", "price": 12.99 },
    ...
    { "id": 20, "name": "Product 20", "price": 20.99 }
  ]
}
```

Alternative techniques, such as embedding pagination details in the request body, can complicate client-server communication and reduce clarity.

Tags: `pagination` `query parameters` `page` `limit` 
<br><br>


### Consider using pagination tokens for large datasets
For large datasets, consider implementing pagination tokens to improve performance and provide a more stable set of results. This
involves returning a token in the response that the client can use to retrieve the next set of results. Tokens ensure that clients
receive a stable set of results, even if the underlying data changes between requests.

**Client Request with Pagination Token**
```http
GET /api/products?limit=10&cursor=abc123
```

**Server Response with Pagination Token**
```http
HTTP/1.1 200 OK
Content-Type: application/json

{
  "limit": 10,
  "nextCursor": "def456",
  "items": [
    { "id": 11, "name": "Product 11", "price": 10.99 },
    { "id": 12, "name": "Product 12", "price": 12.99 },
    ...
    { "id": 20, "name": "Product 20", "price": 20.99 }
  ]
}
```

**Scenarios**
- **Large Collections:** When the collection of resources is large, supporting pagination with tokens prevents overwhelming the client and the server.
- **Changing Data:** When the dataset is frequently updated, pagination tokens ensure that clients receive a consistent view of the data across multiple requests.
- **Efficient Pagination:** Tokens can optimize database queries, reducing the load and improving response times.

**Benefits of Pagination Tokens:**
- **Performance:** More efficient than offset-based pagination for large datasets.
- **Consistency:** Provides stable results even if the underlying data changes.
- **Scalability:** Handles large datasets more effectively.

Tags: `pagination` `pagination tokens` `cursor-based pagination` `query parameters` `large datasets` `performance` `API design` `best practices`
<br><br>


### Always provide metadata in the responses when using pagination
Include metadata such as `totalItems`, `totalPages`, `currentPage`, and `itemsPerPage` in the response to help clients understand the
pagination context. This practice ensures that clients have a clear understanding of the data structure and can navigate large datasets
more effectively.

**Example Request**
```http
GET /api/products?page=2&limit=10
```

**Example Response**
```http
HTTP/1.1 200 OK
Content-Type: application/json

{
  "totalItems": 50,
  "totalPages": 5,
  "currentPage": 2,
  "itemsPerPage": 10,
  "items": [
    { "id": 11, "name": "Product 11", "price": 10.99 },
    { "id": 12, "name": "Product 12", "price": 12.99 },
    ...
    { "id": 20, "name": "Product 20", "price": 20.99 }
  ]
}
```

**Scenarios**
- **Navigating Data**: Clients can use the metadata to determine how many pages of data are available and which page they are currently on.
- **User Interface Design**: Helps in creating user interfaces that show pagination controls, total results, and current page indicators.
- **Optimizing Requests**: Clients can decide if they need to request more data or if they have retrieved all available data based on the metadata.

**Benefits**
- **Clarity**: Provides a clear structure and context for paginated data.
- **User Experience**: Enhances the client's ability to navigate through large datasets efficiently.
- **Efficiency**: Reduces the need for additional requests to determine the size and scope of the dataset.

Tags: `pagination` `metadata` `totalItems` `totalPages` `currentPage` `itemsPerPage`
<br><br>