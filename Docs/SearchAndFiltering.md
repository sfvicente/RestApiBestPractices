# Search and Filtering


## General
<br>


### Always support pagination for search results
Implement pagination in all search result responses to enhance performance and usability, especially when dealing
with large datasets. Pagination divides the data into manageable chunks, reducing server load and improving response
times for clients. Additionally, paginated results improve the user experience by allowing clients to fetch data
progressively rather than retrieving an overwhelming amount of data in a single request.

**Benefits:**
- **Improves performance**: Reduces the volume of data sent in each response, lowering server and client processing times.
- **Enhances user experience**: Allows users to load more data on demand, rather than overwhelming them with all results at once.
- **Supports scalability**: Optimizes server resources for handling large datasets efficiently.

**Example of a Paginated Request:**
```http
GET /api/v1/products?search=laptop&page=2&limit=10
```

In this request:
- `page=2` specifies the page of results.
- `limit=10` restricts the results to 10 items per page.

**Example Response:**
```http
HTTP/1.1 200 OK
Content-Type: application/json

{
  "page": 2,
  "limit": 10,
  "totalResults": 75,
  "totalPages": 8,
  "data": [
    { "id": "11", "name": "Laptop Model A", "price": 900 },
    { "id": "12", "name": "Laptop Model B", "price": 1100 },
    ...
  ]
}
```

In this example, the response includes metadata on the total results and pages, as well as the requested data items for
page 2, giving clients clear insight into pagination status and available results.

<br><br>


### Always return a `200 OK` status code for successful search requests, even if the result set is empty

// TODO: add description

```http
GET https://api.myapi.com/orders?$filter=...
Accept: application/json

HTTP/1.1 200 OK
Content-Type: application/json

{
  ...,
  "value": []
}
```

// TODO: complement description

```http
// TODO: add example
```

<br><br>


### Always use query parameters to allow clients to filter resources

// TODO: add description

```http
GET /api/products?category=electronics
```

<br><br>


### Consider allowing the combination of multiple filter criteria using logical operators

// TODO: add description

```http
GET /api/products?category=electronics&price<100
```

<br><br>


### Consider supporting partial matching and wildcards in search queries

// TODO: add description

```http

```

<br><br>


### Always validate search parameters and return 400 Bad Request for invalid or unsupported filters

// TODO: complement description

```http
// TODO: add example
```

<br><br>


### Always use clear and consistent syntax for filter expressions

// TODO: add description

```http
GET /api/products?price[lt]=100&price[gt]=10
```

<br><br>


### Always provide comprehensive documentation listing all available filters, their data types, and usage examples

// TODO: add description

```http
// TODO: add example
```

<br><br>


### Consider limit the number of filter combinations to avoid performance issues

// TODO: add description

```http
// TODO: add example
```

Tags: `performance`
<br><br>


### Always define and document the default filtering behavior when no filter parameters are specified

// TODO: add description

```http
// TODO: add example
```

<br><br>


### Always validate and sanitize filter inputs to prevent SQL injection and other security vulnerabilities

// TODO: add description

```http
// TODO: add example
```

Tags: `security`
<br><br>


### Consider combining filtering with pagination to manage large datasets

// TODO: add description

```http
GET /api/products?category=electronics&page=2&size=20
```

Tags: `pagination`
<br><br>


### Consider allowing range queries for numerical and date fields

// TODO: add description

**Request**
```http
GET /api/products?price[gte]=10&price[lte]=100
```

<br><br>


### Consider providing sorting options along with filtering

// TODO: add description

**Request**
```http
GET /api/products?category=electronics&sort=price,asc
```

Tags: `sorting`
<br><br>


### Never allow unrestricted search queries

// TODO: add description

**Request**
```http
// TODO: add example
```

<br><br>


### Always return 200 OK for successful filtered requests, even when the result set is empty.
When processing a request that involves filtering resources, the server should always return a `200 OK` status code if the
request is successful, regardless of whether the filtered result set contains any resources. This approach ensures consistency
in API responses and provides clear feedback to the client that the request was processed successfully without any errors.

Returning a `200 OK` status code for an empty result set distinguishes between an empty but valid response and an error
condition. An empty result set is a valid outcome for a request where no resources match the specified criteria.

**Example:**

If a client sends a request to retrieve a list of articles filtered by a specific tag, but there are no articles with
that tag, the server should return a `200 OK` status code with an empty array in the response body.

**Request**
```http
GET /articles?tag=nonexistent-tag
```

- **Request**: Attempts to retrieve articles with a specific tag that does not exist in the database.

**Response**
```http
HTTP/1.1 200 OK
Content-Type: application/json

[]
```

- **Response**: The server responds with a `200 OK` status code, indicating that the request was successful. The response body contains an empty array, signifying that no articles matched the specified tag.

<br><br>


### Always return `400 Bad Request` for invalid filter parameters
When a client sends a request with filter parameters to an endpoint, the server needs to validate these parameters to ensure
they are correct and supported. If the filter parameters are invalid, malformed, or not recognized, the server should respond
with a `400 Bad Request` status code. This indicates to the client that the request was not processed due to incorrect or
inappropriate input and provides an opportunity to correct the request.

**Key Considerations:**

- **Parameter Validation**: The server should validate all incoming filter parameters to ensure they conform to the expected format, data type, and allowable values.
- **Error Message**: Along with the `400 Bad Request` status code, the response should include a descriptive error message detailing which filter parameter(s) were invalid and why. This helps clients identify and correct the specific issue with their request.
- **Consistency**: Consistent handling of invalid parameters across different endpoints makes the API predictable and easier to use, enhancing the overall developer experience.

**Example:**

Consider an API endpoint that allows clients to retrieve a list of articles filtered by a specific date range.

**Request:**

```http
GET /articles?startDate=2024-05-01&endDate=not-a-date
```

- **Request**: The client attempts to retrieve articles filtered by a date range. However, the `endDate` parameter is not in a valid date format.

**Response:**

```http
HTTP/1.1 400 Bad Request
Content-Type: application/json

{
  "error": "Invalid filter parameter",
  "message": "The 'endDate' parameter must be a valid date in the format YYYY-MM-DD."
}
```

- **Response**: The server responds with a `400 Bad Request` status code, indicating that the request was invalid due to the incorrect `endDate` filter parameter. The response includes a detailed error message explaining the problem with the request.

<br><br>


### Consider including metadata such as the total number of filtered items, current page, and page size in the response
When designing an API that supports pagination and filtering, it is helpful to include metadata in the response to provide
additional context about the data being returned. Metadata can include the total number of items that match the filter
criteria, the current page of results, the size of each page, and other relevant information.

Including metadata such as the total number of filtered items, the current page, and the page size provides several benefits:

- **Improved User Experience**: Clients can present more informative interfaces to users, such as displaying the total number of results and providing pagination controls.
- **Enhanced Navigation**: Clients can easily calculate the number of pages available and navigate through them, making it easier to retrieve the desired data.
- **Better Performance Optimization**: Knowing the total number of items and the current page helps clients optimize subsequent requests, particularly when dealing with large datasets.

**Key Considerations:**

- **Total Count**: Include the total number of items that match the filter criteria, even if only a subset of those items is returned in the response.
- **Pagination Details**: Include details about the current page and the size of each page to help clients understand which portion of the dataset is being viewed.
- **Consistent Format**: Ensure that metadata is provided in a consistent format across different endpoints, making the API predictable and easier to use.

**Example:**

Consider an API endpoint that returns a paginated list of articles filtered by a specific category.

**Request:**

```http
GET /articles?category=technology&page=2&pageSize=10
```

- **Request**: The client requests the second page of articles filtered by the "technology" category, with 10 articles per page.

**Response:**

```http
HTTP/1.1 200 OK
Content-Type: application/json

{
  "metadata": {
    "totalItems": 45,
    "pageSize": 10,
    "currentPage": 2,
    "totalPages": 5
  },
  "data": [
    {
      "id": 11,
      "title": "Latest Tech Innovations",
      "content": "An article about the latest in technology...",
      "category": "technology",
      "publishedAt": "2024-05-01T12:00:00Z"
    },
    {
      "id": 12,
      "title": "AI and the Future",
      "content": "Discussing the impact of AI on various industries...",
      "category": "technology",
      "publishedAt": "2024-05-02T15:30:00Z"
    }
    // Additional articles...
  ]
}
```

- **Response**: The server responds with a `200 OK` status code, including metadata that provides information about the total number of items (`totalItems`), the size of each page (`pageSize`), the current page being viewed (`currentPage`), and the total number of pages (`totalPages`). The response also includes the actual data (the list of articles) for the requested page.

This practice enhances the usability of the API by allowing clients to understand the scope of the data and navigate through paginated results efficiently.


<br><br>


### Consider allowing case-insensitive filtering for string fields to improve usability
When designing endpoints that support filtering based on string fields, it is often beneficial to allow case-insensitive
filtering. This provides the following advantages:

- **Improved User Experience**: Users do not have to worry about matching the exact case of the data stored on the server. This can lead to a more seamless and frustration-free interaction with the API.
- **Greater Flexibility**: Allows clients to perform searches without needing to normalize or preprocess user input to match the case of stored data.
- **Consistency Across Applications**: Case-insensitive filtering ensures that applications consuming the API behave consistently, regardless of how user input is formatted or stored data's case sensitivity.

**Key Considerations:**

- **Performance**: Implementing case-insensitive searches might have performance implications depending on the underlying database or data store.
- **Locale Sensitivity**: Consider how different locales might affect case conversion and comparison, especially for non-ASCII characters.
- **Consistency**: Ensure that case-insensitive filtering behavior is consistent across all relevant API endpoints.

**Example:**

Consider an API endpoint that allows clients to filter a list of users by their name. 

**Request:**

```http
GET /users?name=John
```

- **Request**: The client requests to filter the list of users whose names match "John", regardless of the case (e.g., "John", "john", "JOHN", etc.).

**Response:**

```http
HTTP/1.1 200 OK
Content-Type: application/json

{
  "data": [
    {
      "id": 1,
      "name": "John Doe",
      "email": "johndoe@example.com",
      "registeredAt": "2024-01-15T10:00:00Z"
    },
    {
      "id": 2,
      "name": "johnny Appleseed",
      "email": "johnny@example.com",
      "registeredAt": "2024-02-10T14:30:00Z"
    },
    {
      "id": 3,
      "name": "JOHN SMITH",
      "email": "johnsmith@example.com",
      "registeredAt": "2024-03-05T09:20:00Z"
    }
  ]
}
```

- **Response**: The server responds with a `200 OK` status code and returns a list of users whose names match the filter criteria, regardless of the case. The response includes users named "John Doe", "johnny Appleseed", and "JOHN SMITH", demonstrating that the filtering is case-insensitive.

<br><br>


### Never return sensitive data in search results

// TODO: add description

**Request**
```http
// TODO: add example
```

<br><br>


### Consider implementing caching strategies for commonly used filters to enhance performance

// TODO: add description

**Request**
```http
// TODO: add example
```

Tags: `caching`
<br><br>


### Always follow consistent naming conventions for query parameters across the API to improve usability and readability

// TODO: add description

**Request**
```http
// TODO: add example
```

Tags: `naming conventions` `query parameters` `usability` `readability`
<br><br>