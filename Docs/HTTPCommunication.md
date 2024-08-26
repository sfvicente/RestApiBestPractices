# HTTP Communication
HTTP communication in the context of REST APIs involves using standard HTTP methods, also known as verbs, to perform
operations on resources identified by URLs. Each HTTP verb provides a specific action, making REST APIs intuitive and
enabling clear, predictable interactions between clients and servers.

## General Guidelines

...





## HTTP `GET` Method Guidelines
The HTTP GET method is a request method used to retrieve data from a specified resource on the server. It's one of the
most commonly used HTTP methods and is primarily used for fetching information. When a client sends a GET request to a
server, it typically includes parameters in the URL to specify the resource to retrieve or query parameters to filter the results.
<br>


### Always use `GET` requests to read a single resource or a collection of resources.
The `GET` method is used to retrieve representations of resources. `GET` requests are used to fetch data
about a single resource or a collection of resources, and the server responds with the requested data in the body of the
response. Using `GET` for reading resources ensures that clients can obtain the necessary information without causing any side
effects on the server.

**Example**:

#### Example for Single Resource

```http
GET /articles/123
```

- **Request**: Retrieves the article with ID `123`.

```http
HTTP/1.1 200 OK
Content-Type: application/json

{
  "id": 123,
  "title": "An Interesting Article",
  "content": "Lorem ipsum dolor sit amet, consectetur adipiscing elit.",
  "createdAt": "2024-05-15T12:00:00Z",
  "updatedAt": "2024-05-15T12:00:00Z"
}
```

- **Response**: The server responds with a `200 OK` status code and the body contains the details of the article with ID `123`, including its `id`, `title`, `content`, `createdAt`, and `updatedAt` timestamps.

#### Example for Collection of Resources

```http
GET /articles
```

- **Request**: Retrieves the collection of all articles.

```http
HTTP/1.1 200 OK
Content-Type: application/json

[
  {
    "id": 123,
    "title": "An Interesting Article",
    "content": "Lorem ipsum dolor sit amet, consectetur adipiscing elit.",
    "createdAt": "2024-05-15T12:00:00Z",
    "updatedAt": "2024-05-15T12:00:00Z"
  },
  {
    "id": 124,
    "title": "Another Article",
    "content": "Vestibulum ante ipsum primis in faucibus orci luctus et.",
    "createdAt": "2024-05-16T08:00:00Z",
    "updatedAt": "2024-05-16T08:00:00Z"
  }
]
```

- **Response**: The server responds with a `200 OK` status code and the body contains an array of articles, each with its details such as `id`, `title`, `content`, `createdAt`, and `updatedAt` timestamps.

It is a safe and idempotent HTTP method, meaning it does not alter the state of the resource and repeated requests will produce
the same result.

Tags: `HTTP methods` `GET` `resource retrieval` `REST API design` `idempotent` `safe operations`
<br>


### Always return a `404 Not Found` status for `GET` requests to non-existent individual resources.
When a `GET` request is made for an individual resource that is not found on the server, the API should return
a `404 Not Found` status code. This informs the client that the requested resource does not exist, ensuring clarity
and consistency in API behavior.

**Example**:

```http
GET /articles/123
```

- **Request**: Attempts to retrieve the article with ID `123`.

```http
HTTP/1.1 404 Not Found
Content-Type: application/json

{
  "error": "Resource not found",
  "message": "The requested article with ID '123' does not exist."
}
```

- **Response**: The server responds with a `404 Not Found` status code along with a JSON payload providing details
about the error. This communicates to the client that the requested article could not be found.

<br><br>


### Always return a `200 OK` status for `GET` requests to collection resources, even if the collection is empty.
When clients make `GET` requests to retrieve a collection of resources, the API should return a `200 OK` status code
even if the collection is empty. This indicates that the request was successfully processed, and the response body 
will contain an empty array or object representing the collection.

**Example**:

```http
GET /articles
```

- **Request**: Retrieves the collection of articles.

```http
HTTP/1.1 200 OK
Content-Type: application/json

{
  "articles": []
}
```

- **Response**: The server responds with a `200 OK` status code, indicating that the request was successful. The response
body contains an empty array (`"articles": []`), indicating that there are no articles in the collection.

Tags: `HTTP methods` `GET` `404 Not Found` `resource retrieval` `collection handling` `error handling` `empty collection` `consistent responses`
<br><br>


### Always return a `404 Not Found` status for `GET` requests if the requested collection resource is missing.
When clients make `GET` requests to retrieve a collection of resources and the requested collection does not exist
(i.e., it has not been implemented or configured), the API should return a `404 Not Found` status code. This communicates
to the client that the requested endpoint or resource is not available, distinguishing between an empty collection (which
should return `200 OK` with an empty response) and a missing or undefined collection.

**Example**:

```http
GET /articles
```

- **Request**: Attempts to retrieve the collection of articles.

```http
HTTP/1.1 404 Not Found
Content-Type: application/json

{
  "error": "Resource not found",
  "message": "The requested collection '/articles' does not exist."
}
```

- **Response**: The server responds with a `404 Not Found` status code along with a JSON payload providing details about the error. This informs the client that the requested collection (`/articles`) is not available or has not been implemented.

This ensures consistent and meaningful responses for `GET` requests to collection resources, enhancing the clarity and
reliability of API interactions. This practice helps clients differentiate between different states of resource availability,
improving overall usability and error handling.

Tags: `HTTP methods` `GET` `404 Not Found` `collection retrieval` `resource handling` `error handling` `missing resources` `consistent responses`
<br><br>


### Always provide adequate filtering and pagination mechanisms for `GET` requests on collection resources.

// TODO: add description.

```http
// TODO: add example
```

See also: Filtering, Pagination
<br><br>



## HTTP `POST` Method Guidelines
The HTTP POST method is a request method used to submit data to be processed by a specified resource on the
server. It's commonly used when creating new resources or when submitting data to a server that will trigger
a specific action. Unlike GET requests, which retrieve data, POST requests typically include data in the request
body, allowing for more complex data transmission.
<br>


### Always generate a `200` status code for successful `POST` requests when resources have been updated.
When clients make `POST` requests to create or update resources, the API should return a `200 OK` status code if the
request was successful and resulted in the modification or creation of resources. This indicates that the operation
was completed successfully, and the response body may include details about the updated resources.

**Example**:

```http
POST /articles
Content-Type: application/json

{
  "title": "New Article",
  "content": "Lorem ipsum dolor sit amet, consectetur adipiscing elit."
}
```

- **Request**: Creates a new article with the specified title and content.

```http
HTTP/1.1 200 OK
Content-Type: application/json

{
  "id": 123,
  "title": "New Article",
  "content": "Lorem ipsum dolor sit amet, consectetur adipiscing elit.",
  "createdAt": "2024-05-15T12:00:00Z",
  "updatedAt": "2024-05-15T12:00:00Z"
}
```

- **Response**: The server responds with a `200 OK` status code, indicating that the `POST` request was successful and the article was created. The response body contains the details of the newly created article, including its `id`, `title`, `content`, `createdAt`, and `updatedAt` timestamps.

Using `200 OK` for successful `POST` requests aligns with HTTP semantics and communicates the successful modification of
resources to clients. This provides clear and consistent feedback to clients about the outcome of `POST` requests,
enabling them to handle resource creation or update operations effectively. This practice enhances the usability and
reliability of your API design.

Tags: `HTTP methods` `POST` `200 OK` `resource creation` `resource update` `success responses` `resource modification` `API usability` `consistent feedback`
<br><br>


### Always generate a `201 Created` status code for successful `POST` requests when new resources have been created.
When clients make `POST` requests to create new resources, the API should return a `201 Created` status code upon
successful creation. This status code indicates that the request was successful and that a new resource has been 
created on the server.

**Example**:

```http
POST /articles
Content-Type: application/json

{
  "title": "New Article",
  "content": "Lorem ipsum dolor sit amet, consectetur adipiscing elit."
}
```

- **Request**: Creates a new article with the specified title and content.

```http
HTTP/1.1 201 Created
Content-Type: application/json
Location: /articles/123

{
  "id": 123,
  "title": "New Article",
  "content": "Lorem ipsum dolor sit amet, consectetur adipiscing elit.",
  "createdAt": "2024-05-15T12:00:00Z",
  "updatedAt": "2024-05-15T12:00:00Z"
}
```

- **Response**: The server responds with a `201 Created` status code, indicating that the `POST` request was successful
and a new article has been created. The `Location` header provides the URI of the newly created article (`/articles/123`).
The response body includes the details of the newly created article, such as its `id`, `title`, `content`, and timestamps.

Tags: `HTTP methods` `POST` `201 Created` `resource creation` `success responses` `Location header` `new resource` `API usability` `resource management`
<br><br>


### Always include the URI of the newly created resource in the `Location` header for successful `POST` requests.
When a `POST` request successfully creates a new resource, it is a best practice to include the URI of the newly created
resource in the `Location` header of the response. This provides clients with a direct link to the new resource, allowing
them to easily access, retrieve, or interact with it. 

**Example**:

```http
POST /articles
Content-Type: application/json

{
  "title": "New Article",
  "content": "Lorem ipsum dolor sit amet, consectetur adipiscing elit."
}
```

- **Request**: Creates a new article with the specified title and content.

```http
HTTP/1.1 201 Created
Content-Type: application/json
Location: /articles/123

{
  "id": 123,
  "title": "New Article",
  "content": "Lorem ipsum dolor sit amet, consectetur adipiscing elit.",
  "createdAt": "2024-05-15T12:00:00Z",
  "updatedAt": "2024-05-15T12:00:00Z"
}
```

- **Response**: The server responds with a `201 Created` status code, indicating that the `POST` request was successful
and a new article has been created. The `Location` header provides the URI of the newly created article (`/articles/123`).
The response body includes the details of the newly created article, such as its `id`, `title`, `content`, and timestamps.

Including the `Location` header improves the usability of the API by giving clients immediate knowledge of the new resource's
URI, which can be useful for subsequent operations such as `GET`, `PUT`, `PATCH`, or `DELETE` requests on that resource.

Tags: `HTTP methods` `POST` `Location header` `resource creation` `201 Created` `URI` `API usability` `best practices` `new resource`
<br><br>


### Always include a representation of the newly created resource in the response body for successful `POST` requests.

// TODO: add description.

```http
// TODO: add example
```

<br><br>

### Consider returning a `202` status code for successful `POST` requests when the request is accepted but processing is not yet complete.

// TODO: add description.

```http
// TODO: add example
```

<br><br>


### Consider generating a `204` status code with a `Location` header for successful `POST` requests when the actual resource is not returned.

// TODO: add description.

```http
// TODO: add example
```

<br><br>


### Never pass resource IDs in `POST` requests when creating new resources.

Resource IDs should be created and maintained by the API and returned with the response payload.

// TODO: complement description.

```http
// TODO: add example
```

<br><br>


### Consider designing `POST` operations as idempotent.
While the HTTP `POST` method is traditionally used for creating new resources or triggering operations that result
in a state change, it is often beneficial to design `POST` operations to be idempotent where possible. Idempotency
ensures that making the same request multiple times will produce the same result, improving reliability and user
experience.

**Benefits of Idempotent `POST` Operations:**

- **Consistency**: Clients can safely retry requests without risking unintended side effects, which is especially useful in unreliable network conditions.
- **Error Handling**: Reduces the complexity of error handling and recovery, as the same request can be retried without concern for duplication or inconsistencies.
- **Predictability**: Enhances predictability of the API behavior, making it easier for clients to understand and work with the API.

**Examples of Idempotent `POST` Operations:**

- **Order Processing**: An API endpoint that processes an order could be designed to be idempotent by ensuring that submitting the same order multiple times has the same effect as submitting it once.
- **Payment Transactions**: A payment API might handle duplicate requests for the same transaction by ensuring that only one payment is processed, even if the request is sent multiple times.

**Considerations:**

- **Resource Creation**: For resource creation, idempotency might require using a unique identifier or key provided by the client to ensure that multiple submissions do not result in multiple resources being created.
- **Operation Triggering**: For operations that trigger external processes, careful design is needed to ensure that multiple identical requests do not result in unintended side effects.

Tags: `HTTP methods` `POST` `idempotency` `reliability` `error handling` `consistency` `predictability`
<br><br>



## HTTP `PUT` Method Guidelines
The HTTP PUT method is a request method used to update or replace a resource on the server with the representation
enclosed in the request payload. It's commonly employed when the client intends to update an existing resource or
create a new one if it doesn't exist. PUT typically replaces the entire resource with the new representation provided
in the request.
<br>


### Always use `PUT` requests to update complete individual or collection resources
When updating resources through an API, the `PUT` method should be used to ensure that the operation is clear, consistent,
and aligns with HTTP semantics. The `PUT` method is designed to update a resource at a specific URI, and it is intended
for cases where the client sends a complete representation of the resource, whether it is an individual resource or a
collection.

**Key Points for Using `PUT` Requests:**
- **Complete Replacement**: A `PUT` request should contain a full representation of the resource to replace the existing resource at the target URI. If only partial updates are needed, consider using the `PATCH` method instead.
- **Idempotency**: `PUT` requests are idempotent, meaning that sending the same `PUT` request multiple times will result in the same state on the server. This is crucial for ensuring consistency, especially in environments with unreliable network conditions.
- **Specificity**: The `PUT` method is specific to the resource identified by the URI. Whether updating an individual resource or a collection, the request should target the exact URI where the resource resides.

**Examples of `PUT` Requests:**

- **Updating an Individual Resource**: If the client needs to update a user profile, the `PUT` request should include the entire profile data, replacing the existing profile at the specified URI.

  ```http
  PUT /users/123
  Content-Type: application/json

  {
    "id": 123,
    "name": "John Doe",
    "email": "john.doe@example.com",
    "age": 30,
    "address": "123 Elm Street, Springfield"
  }
  ```

  - **Request**: The above request updates the user profile for the user with ID `123`. The server will replace the existing user profile data with the data provided in the request.

  ```http
  HTTP/1.1 200 OK
  Content-Type: application/json

  {
    "id": 123,
    "name": "John Doe",
    "email": "john.doe@example.com",
    "age": 30,
    "address": "123 Elm Street, Springfield",
    "updatedAt": "2024-08-19T12:00:00Z"
  }
  ```

  - **Response**: The server responds with a `200 OK` status code, indicating that the user profile was successfully updated. The response body includes the updated user profile with a timestamp.

- **Updating a Collection**: When updating an entire collection of resources, the `PUT` request should include the complete set of resources that will replace the current collection at the target URI.

  ```http
  PUT /articles
  Content-Type: application/json

  [
    {
      "id": 101,
      "title": "First Article",
      "content": "Content of the first article.",
      "createdAt": "2024-08-15T12:00:00Z",
      "updatedAt": "2024-08-19T12:00:00Z"
    },
    {
      "id": 102,
      "title": "Second Article",
      "content": "Content of the second article.",
      "createdAt": "2024-08-16T08:00:00Z",
      "updatedAt": "2024-08-19T12:00:00Z"
    }
  ]
  ```

  - **Request**: The above request updates the entire collection of articles, replacing the existing collection with the two articles provided in the request.

  ```http
  HTTP/1.1 200 OK
  Content-Type: application/json

  [
    {
      "id": 101,
      "title": "First Article",
      "content": "Content of the first article.",
      "createdAt": "2024-08-15T12:00:00Z",
      "updatedAt": "2024-08-19T12:00:00Z"
    },
    {
      "id": 102,
      "title": "Second Article",
      "content": "Content of the second article.",
      "createdAt": "2024-08-16T08:00:00Z",
      "updatedAt": "2024-08-19T12:00:00Z"
    }
  ]
  ```

  - **Response**: The server responds with a `200 OK` status code, indicating that the collection was successfully updated. The response body includes the updated collection of articles with timestamps.


**Considerations:**
- **Conflict Management**: If a resource does not exist at the specified URI, the server may either create a new resource or return an error, depending on the API design. It is important to define how your API handles such cases.
- **Data Integrity**: Since `PUT` replaces the resource entirely, clients must ensure that they send a complete and accurate representation of the resource to avoid unintentional data loss.

<br><br>


### Ensure `PUT` requests handle non-existent resources by implicitly creating them before updating.
When clients make `PUT` requests to update a resource at a specific URI, the API should be robust against the non-existence
of the resource by implicitly creating it before performing the update. This means that if the resource identified by the
URI does not already exist, the API should create it based on the provided data in the `PUT` request payload.

**Example**:

```http
PUT /articles/123
Content-Type: application/json

{
  "title": "Updated Article",
  "content": "Updated content."
}
```

- **Request**: Attempts to update the article with ID `123`. If the article does not exist, the API should implicitly create it with the provided data.

```http
HTTP/1.1 200 OK
Content-Type: application/json

{
  "id": 123,
  "title": "Updated Article",
  "content": "Updated content.",
  "createdAt": "2024-05-15T12:00:00Z",
  "updatedAt": "2024-05-15T12:05:00Z"
}
```

- **Response**: The server responds with a `200 OK` status code, indicating that the `PUT` request was successful. If the article did not exist previously, it is created with the specified `title`, `content`, `createdAt`, and `updatedAt` timestamps. If the article already existed, it is updated with the provided data.

By implementing this guideline, an API provides flexibility and robustness in handling `PUT` requests, allowing clients
to use the same method for both creating and updating resources at specific URIs. This practice simplifies API usage,
ensures consistency and predictability in API interactions and improves the overall developer experience. However, note
that this behavior may vary based on specific use cases and API requirements.

Tags: `HTTP methods` `PUT` `resource creation` `resource update` `idempotence` `API robustness` `resource handling` `developer experience` `best practices`
<br><br>


### Always perform a full resource replacement with the payload on a successful `PUT` request.
When handling a `PUT` request, the API should replace the entire resource at the specified URL with the data provided
in the request payload. This ensures that the resource is fully updated according to the client's submission, with any
missing fields in the payload leading to their corresponding fields in the resource being removed or set to their default
values. The `PUT` method is intended for complete updates, meaning that the server should ensure that subsequent reads
of the resource reflect exactly the content sent by the client in the `PUT` request.

**Guidelines for Implementing `PUT` Requests:**

- **Full Replacement**: The payload should include all necessary fields of the resource. Any field not included will be considered as absent or to be reset.
- **Idempotence**: `PUT` requests should be idempotent, meaning that making the same `PUT` request multiple times will have the same effect as making it once. The resource's state will not change after the first successful request unless the payload changes.
- **Validation**: Ensure that the server validates the incoming payload to confirm that it includes all required fields and adheres to the expected schema.

**Example of a `PUT` Request:**

Consider a scenario where a client wants to update an article with ID `123`. The client sends a `PUT` request to update the entire article, providing a full representation of the article in the request payload.

```http
PUT /articles/123 HTTP/1.1
Host: api.example.com
Content-Type: application/json

{
  "title": "Updated Article Title",
  "content": "This is the updated content of the article.",
  "author": "John Doe",
  "tags": ["update", "PUT", "api"]
}
```

- **Request**: The client sends a `PUT` request to the `/articles/123` endpoint, providing the updated representation of the article, including the `title`, `content`, `author`, and `tags`.

**Example Response:**

```http
HTTP/1.1 200 OK
Content-Type: application/json

{
  "id": 123,
  "title": "Updated Article Title",
  "content": "This is the updated content of the article.",
  "author": "John Doe",
  "tags": ["update", "PUT", "api"],
  "createdAt": "2024-05-15T12:00:00Z",
  "updatedAt": "2024-05-16T14:00:00Z"
}
```

- **Response**: The server responds with a `200 OK` status code, confirming that the article was successfully updated. The response body contains the full representation of the updated article, reflecting the exact content that was provided in the request payload.

**Benefits of This Approach:**

- **Consistency**: The state of the resource after a `PUT` request is guaranteed to be consistent with the data provided by the client, eliminating partial updates and potential discrepancies.
- **Clarity**: Ensures clear and predictable behavior of the API by adhering to the HTTP specification for the `PUT` method, which is defined as a complete replacement of the target resource.
- **Simplifies Client Logic**: Clients can update a resource without needing to worry about the previous state. They can simply send the full, updated representation of the resource.

- 
- <br><br>


### Always return a `200 OK` status for successful `PUT` requests when the updated content is returned.
When a `PUT` request is successfully processed and the resource is updated, the API should return a `200 OK` status
code. This indicates that the update operation was successful, and the response should include the actual content of
the updated resource. By returning the updated resource in the response body, the API ensures that the client has the
most recent version of the resource, providing immediate feedback on the changes made.

Using a `200 OK` status code along with the updated content enhances clarity in the API's communication, confirming
to the client that the update was performed and allowing them to see the exact state of the resource post-update. This
practice contributes to better client experience, as it eliminates the need for an additional `GET` request to retrieve
the updated resource.

```http
PUT /articles/123
Content-Type: application/json

{
  "title": "Updated Article",
  "content": "Updated content."
}
```

- **Request**: Attempts to update the article with ID `123`.

```http
HTTP/1.1 200 OK
Content-Type: application/json

{
  "id": 123,
  "title": "Updated Article",
  "content": "Updated content.",
  "createdAt": "2024-05-15T12:00:00Z",
  "updatedAt": "2024-05-15T12:10:00Z"
}
```

- **Response**: The server responds with a `200 OK` status code and returns the updated content of the article, including the `id`, `title`, `content`, `createdAt`, and `updatedAt` timestamps.

This approach ensures transparency in API interactions and reduces the likelihood of discrepancies between the client and
server's understanding of the resource's current state.

Tags: `HTTP methods` `PUT` `status codes` `200 OK` `resource updates`
<br><br>



### Always return a `204` status code for successful `PUT` requests when the resource is updated without actual content returned.
When a `PUT` request is made to update a resource and the operation is successful, but there is no need to return any content
in the response body, the API should return a `204 No Content` status code. This indicates that the request was successfully
processed, the resource was updated, and there is no additional content to send in the response. This approach is efficient,
reduces bandwidth usage, and aligns with HTTP standards.

**Example**:

```http
PUT /articles/123
Content-Type: application/json

{
  "title": "Updated Article",
  "content": "Updated content."
}
```

- **Request**: Updates the article with ID `123` with the specified title and content.

```http
HTTP/1.1 204 No Content
```

- **Response**: The server responds with a `204 No Content` status code, indicating that the article was successfully updated but no further content is returned in the response body.

<br><br>



## HTTP `DELETE` Method Guidelines
The HTTP DELETE method is a standard HTTP request method used to delete a specified resource on a server. When a client sends a
DELETE request, it instructs the server to remove the resource identified by the URI. This method is idempotent, meaning that
multiple identical requests have the same effect as a single request. 
<br>


### Consider generating an HTTP `200` return code on a successful `DELETE` request if the deleted resource is returned after executing the request.
When a `DELETE` request is made to remove a resource, and the API is designed to return the details of the deleted resource
in the response, it is appropriate to return a `200 OK` status code. This informs the client that the resource was successfully
deleted and provides the relevant resource information as part of the response body.

**Example**:

```http
DELETE /articles/123
```

- **Request**: Deletes the article with ID `123`.

```http
HTTP/1.1 200 OK
Content-Type: application/json

{
  "id": 123,
  "title": "Deleted Article",
  "content": "This article has been deleted.",
  "deletedAt": "2024-05-15T12:00:00Z"
}
```

- **Response**: The server responds with a `200 OK` status code, indicating that the article was successfully deleted. The response body contains the details of the deleted article, including its `id`, `title`, `content`, and the timestamp of deletion (`deletedAt`).

Tags: `HTTP methods` `DELETE` `status codes` `200 OK` `resource deletion`
<br>


### Prefer generating an HTTP `204` return code on a successful `DELETE` request if no further information is returned after executing the request.
When no content is returned after a delete operation successfully executes, an HTTP status code 204 should be returned. This indicates that the
process has been successfully handled, however, the body of the response does not contain additional information.

// TODO: complement description

```http
// TODO: add example
```

<br><br>


### Always ensure that `DELETE` operations are idempotent
For `DELETE` operations, if a client issues a `DELETE` request for a resource, repeating the request should not cause an
error or additional changes—the resource should be deleted the first time, and subsequent requests should confirm that
the resource is already deleted.

**Key Points for Idempotent `DELETE` Operations:**

- **Consistency**: Once a resource is deleted, subsequent `DELETE` requests to the same URI should return a status that indicates the resource is no longer available, rather than attempting to delete it again.
- **Error Handling**: The server should handle repeated `DELETE` requests gracefully, returning a response that clearly communicates the resource's state without causing unnecessary errors.

**Examples of Idempotent `DELETE` Requests:**

- **Initial `DELETE` Request**: A client issues a `DELETE` request to remove a specific resource.

  ```http
  DELETE /articles/123
  HTTP/1.1
  Host: api.example.com
  ```

  - **Request**: This request attempts to delete the article with ID `123`.

  ```http
  HTTP/1.1 200 OK
  Content-Type: application/json

  {
    "message": "Article successfully deleted."
  }
  ```

  - **Response**: The server responds with a `200 OK` status code, indicating that the article was successfully deleted. The response body provides confirmation of the deletion.

- **Subsequent `DELETE` Request for the Same Resource**: A client issues the same `DELETE` request after the resource has already been deleted.

  ```http
  DELETE /articles/123
  HTTP/1.1
  Host: api.example.com
  ```

  - **Request**: This request attempts to delete the same article with ID `123`, which has already been deleted.

  ```http
  HTTP/1.1 404 Not Found
  Content-Type: application/json

  {
    "error": "Resource not found",
    "message": "The article with ID '123' has already been deleted or does not exist."
  }
  ```

  - **Response**: The server responds with a `404 Not Found` status code, indicating that the article with ID `123` no longer exists. The response body informs the client that the resource has already been deleted or was never present.

**Considerations:**

- **Graceful Handling**: Ensure that repeated `DELETE` requests do not cause server errors or unnecessary processing. The response should indicate that the resource is no longer present without causing confusion.
- **Clear Communication**: Responses should clearly communicate the outcome of the `DELETE` request, whether it was the initial deletion or a subsequent confirmation that the resource no longer exists.

See also: Idempotency
<br><br>



## HTTP `PATCH` Method Guidelines
The HTTP PATCH method is a request method used to apply partial modifications to a resource on a server. Unlike the PUT
method, which updates the entire resource, PATCH allows for more fine-grained updates, modifying only the specified parts
of the resource. This method is not necessarily idempotent, as applying the same patch multiple times can result in
different outcomes.
<br>


### Always use PATCH for partial updates to resources.

// TODO: add description.

```http
// TODO: add example
```

<br><br>


### Always use `PATCH` requests for updating an existing object incrementally.
`PATCH` requests are used to apply partial updates to an existing resource. Unlike `PUT` requests, which replace the entire
resource with the new data, `PATCH` requests allow clients to send only the changes or updates that need to be applied. This
makes `PATCH` ideal for scenarios where only specific fields of a resource need to be modified without affecting the entire
resource.

**Example**:

```http
PATCH /users/123
Content-Type: application/json

{
  "email": "newemail@example.com"
}
```

- **Request**: Updates the email address of the user with ID `123`. Only the `email` field is provided, indicating that this is the only field to be updated.

```http
HTTP/1.1 200 OK
Content-Type: application/json

{
  "id": 123,
  "username": "johndoe",
  "email": "newemail@example.com",
  "createdAt": "2023-01-10T08:00:00Z",
  "updatedAt": "2024-05-15T12:10:00Z"
}
```

- **Response**: The server responds with a `200 OK` status code, indicating that the `PATCH` request was successful. The response body contains the updated user resource, showing that only the `email` field was modified, while other fields remain unchanged.

Using `PATCH` for incremental updates ensures efficient use of network resources and minimizes the risk of unintentional
data loss. It allows for efficient and precise updates to resources, reducing unnecessary data transfer and
preserving the integrity of existing data. Clients can perform targeted updates without the risk of overwriting
unintended parts of a resource.

References: [RFC 5789](https://datatracker.ietf.org/doc/html/rfc5789)
<br><br>


### Consider designing `PATCH` operations as idempotent.
While the HTTP `PATCH` method is typically used to apply partial updates to a resource, it is beneficial to 
design `PATCH` operations to be idempotent whenever possible. An idempotent `PATCH` operation ensures that
multiple identical requests will have the same effect as a single request. This characteristic is important
for enhancing the reliability and predictability of an API, especially in environments where network issues
or client errors may lead to the same request being sent multiple times.

**Benefits of Idempotent `PATCH` Operations:**

- - **Consistency**: Ensures that multiple identical `PATCH` requests will not result in unintended changes to the resource, maintaining the consistency of the resource's state.
- **Error Handling**: Simplifies error handling and recovery processes, as clients can safely retry requests without concern for creating inconsistencies.
- **Predictability**: Enhances the predictability of the API's behavior, making it easier for developers to understand and interact with the API effectively.

**Examples of Idempotent `PATCH` Operations:**

Consider a scenario where a user wants to update their profile information, such as their email address:

**Example**:

```http
PATCH /users/123
Content-Type: application/json

{
  "email": "newemail@example.com"
}
```

- **Request**: Updates the email address of the user with ID `123`.

```http
HTTP/1.1 200 OK
Content-Type: application/json

{
  "id": 123,
  "email": "newemail@example.com",
  "updatedAt": "2024-05-15T12:10:00Z"
}
```

- **Response**: The server responds with a `200 OK` status code, indicating that the `PATCH` request was successful. The response body includes the updated email address and the timestamp of the update.

If the client sends the same `PATCH` request multiple times, the user's email address remains unchanged after the first
update. The subsequent requests have no additional effect, demonstrating the idempotent nature of the `PATCH` operation.

<br><br>


### Ensure PATCH requests are atomic to maintain data consistency.

// TODO: add description.

```http
// TODO: add example
```

<br><br>


### Implement mechanisms to handle concurrent PATCH modifications.

// TODO: add description.

```http
// TODO: add example
```

<br><br>


## HTTP `HEAD` Method Guidelines
The HTTP HEAD method is a request method used to retrieve the headers of a specified resource, without fetching the actual
body content. When a client sends a HEAD request, the server responds with the same headers it would send for a GET request,
but without the response body. This method is useful for checking metadata, such as content type and size, or testing if a
resource exists (via the status code) without downloading the entire resource
<br>


### Always use `HEAD` requests to retrieve header information of single resource or a collections of resources.
The `HEAD` method returns the metadata of an object for a `GET` response. It is an idempotent operation.

The `HEAD` method is used to retrieve the headers of a resource without fetching the actual body. This is useful
for obtaining metadata about a resource, such as its size, content type, or last modified date, without transferring
the entire resource representation. Using `HEAD` requests can improve performance and reduce bandwidth usage, 
particularly when clients only need to check the headers before making decisions about further actions.

**Example**:

#### Example for Single Resource

```http
HEAD /articles/123
```

- **Request**: Retrieves header information for the article with ID `123`.

```http
HTTP/1.1 200 OK
Content-Type: application/json
Content-Length: 1234
Last-Modified: Mon, 15 May 2024 12:00:00 GMT
ETag: "abc123"
```

- **Response**: The server responds with the headers that describe the article with ID `123`, including `Content-Type`, `Content-Length`, `Last-Modified`, and `ETag`. The response does not include the body of the article.

#### Example for Collection of Resources

```http
HEAD /articles
```

- **Request**: Retrieves header information for the collection of articles.

```http
HTTP/1.1 200 OK
Content-Type: application/json
Content-Length: 5678
Last-Modified: Mon, 15 May 2024 12:00:00 GMT
ETag: "def456"
```

- **Response**: The server responds with headers that describe the collection of articles, including `Content-Type`, `Content-Length`, `Last-Modified`, and `ETag`. The response does not include the body of the articles collection.

The response to a `HEAD` request should be identical to that of a corresponding `GET` request, except that it does not contain a
response body.

See also: Idempotency
<br><br>


### Consider using `HEAD` to efficiently lookup whether large resources or collection resources have been updated in conjunction with the `ETag` header.

// TODO: add description.

```http
// TODO: add example
```

See also: Concurrency
<br><br>



## HTTP `OPTIONS` Method Guidelines
The HTTP OPTIONS method is a request method used to describe the communication options available for a specified resource
or the server as a whole. When a client sends an OPTIONS request, the server responds with the allowed HTTP methods (such as
GET, POST, PUT, DELETE) that can be performed on the resource. This method is useful for determining the capabilities of a
server or resource, often used in the context of Cross-Origin Resource Sharing (CORS) to check permitted operations before
making actual requests.
<br>


### Always use `OPTIONS` requests to inspect the available operations of a specific endpoint.
The `OPTIONS` HTTP method is an important tool that allows clients to query a server to discover the HTTP methods that are
supported by a specific resource or endpoint. By using an `OPTIONS` request, clients can determine which operations (such
as `GET`, `POST`, `PUT`, `DELETE`, etc.) are available for a given endpoint, as well as any additional communication options,
such as CORS (Cross-Origin Resource Sharing) permissions.

**Benefits of Using `OPTIONS` Requests:**

- **Discoverability**: Helps clients understand what operations are allowed or supported for a specific endpoint, making the API more self-explanatory and easier to use.
- **Error Prevention**: By querying available options before performing a request, clients can prevent errors related to unsupported operations or invalid HTTP methods.
- **CORS Support**: The `OPTIONS` request is commonly used in CORS preflight requests to determine if the actual request is safe to send. This is particularly important for cross-origin requests in web applications.

**Usage of `OPTIONS` Requests:**

The `OPTIONS` request should be used when a client wants to check the allowed methods for a resource, determine supported
content types, or find out more about the server's capabilities for a particular endpoint.

**Example of an `OPTIONS` Request:**

Consider a scenario where a client wants to find out what operations are available on the `/articles` endpoint:

```http
OPTIONS /articles HTTP/1.1
Host: api.example.com
```

- **Request**: The client sends an `OPTIONS` request to the `/articles` endpoint to determine the supported methods and operations.

**Example Response:**

```http
HTTP/1.1 200 OK
Allow: GET, POST, PUT, DELETE, OPTIONS
Access-Control-Allow-Origin: *
Access-Control-Allow-Methods: GET, POST, PUT, DELETE, OPTIONS
Content-Type: application/json
```

- **Response**: The server responds with a `200 OK` status code, indicating that the request was successful. The `Allow` header in the response lists the HTTP methods that are supported for the `/articles` endpoint (`GET`, `POST`, `PUT`, `DELETE`, `OPTIONS`). Additionally, the response may include other headers, such as `Access-Control-Allow-Origin` and `Access-Control-Allow-Methods`, which are important for handling CORS requests.

See also: HTTP Methods
<br><br>


## HTTP 'TRACE' Method Guidelines
The HTTP TRACE method is a request method used for diagnostic purposes, allowing the client to see what is being received
at the other end of the request chain and to use that data for testing or debugging. When a client sends a TRACE request,
the server echoes back the received request so the client can see any modifications or additions made by intermediate
servers. This method helps in identifying potential issues in the request path, such as changes made by proxies.
<br>


### Consider using the `TRACE` method to debug or troubleshoot web server connections.
The `TRACE` method is a useful tool for debugging and troubleshooting web server connections during the development
phase. It echoes the contents of an HTTP request back to the requester, allowing developers to see the exact request
received by the server and verify that the server is processing requests correctly.

**Usage Scenario:**
- **Development and Debugging**: During development, the `TRACE` method can help developers ensure that HTTP requests are being correctly received and processed by the server. It can reveal issues with request formatting, headers, and other request attributes.

**Security Considerations:**
- **Disable in Production**: While useful in development, the `TRACE` method should be disabled in production environments to prevent potential security risks such as Cross-Site Tracing (XST) attacks.

**Example Request and Response:**
```http
// Request
TRACE /trace HTTP/1.1
Host: example.com
User-Agent: curl/7.64.1
Accept: */*

// Response
HTTP/1.1 200 OK
Content-Type: message/http

TRACE /trace HTTP/1.1
Host: example.com
User-Agent: curl/7.64.1
Accept: */*
```

**Tags:** `debugging` `development` `HTTP methods` `TRACE` `troubleshooting` `best practices`
<br><br>


### Always disable the `TRACE` method for security reasons, unless specifically required.
The HTTP `TRACE` method should be disabled in your API to prevent potential security vulnerabilities. The
`TRACE` method is primarily used for diagnostic purposes, allowing clients to see the exact request sent to
the server and the server's response. However, it can be exploited by malicious users to access sensitive
information in HTTP headers, such as cookies and authentication tokens.

**Security Risks:**
- **Cross-Site Tracing (XST) Attacks**: Attackers can exploit `TRACE` to steal credentials or session information by tricking the client into sending a request that reveals sensitive data.
- **Information Leakage**: `TRACE` can expose internal implementation details and HTTP headers that should remain confidential.

**Example Request and Response:**
```http
// Request
TRACE /api/resource HTTP/1.1
Host: example.com

// Response (when TRACE is disabled)
HTTP/1.1 405 Method Not Allowed
Content-Type: application/json

{
  "error": "Method Not Allowed",
  "message": "The TRACE method is disabled for security reasons."
}
```

**Tags:** `security` `HTTP methods` `TRACE` `vulnerability` `best practices`
<br><br>



## HTTP Status Codes Guidelines
<br>


### Always use the most specific HTTP status codes for returning information regarding request and error handling.
When returning information to clients regarding request or error handling, the API should use the most specific 
HTTP status code possible. This practice ensures clear communication between the server and the client, helping
clients understand the exact nature of the response and how to handle it appropriately.

**Benefits of Using Specific HTTP Status Codes:**
- **Clarity**: Specific status codes provide precise information about the outcome of the request, reducing ambiguity.
- **Troubleshooting**: Clear status codes make it easier to diagnose issues and understand the cause of errors.
- **Client Handling**: Clients can implement more accurate error handling and responses based on specific status codes.

**Examples:**
- **400 Bad Request**: Use when the request cannot be processed due to client-side errors, such as validation issues.
  ```http
  HTTP/1.1 400 Bad Request
  Content-Type: application/json

  {
    "error": "Bad Request",
    "message": "Invalid input data"
  }
  ```
- **401 Unauthorized**: Use when authentication is required and has failed or not been provided.
  ```http
  HTTP/1.1 401 Unauthorized
  Content-Type: application/json

  {
    "error": "Unauthorized",
    "message": "Authentication required"
  }
  ```
- **404 Not Found**: Use when the requested resource could not be found.
  ```http
  HTTP/1.1 404 Not Found
  Content-Type: application/json

  {
    "error": "Not Found",
    "message": "Resource not found"
  }
  ```

**Tags:** `HTTP status codes` `error handling` `client communication`
<br><br>


### Always use HTTP `4XX` return codes for malformed requests, when the issue is on the client's side.
HTTP `4XX` status codes should always be used to indicate that a request is malformed or cannot be processed due
to issues on the client's side. These status codes inform the client that the server has understood the request,
but it cannot process it due to client-related errors. 

**Key Points for Using `4XX` Status Codes:**

- **Client-Side Errors:** `4XX` status codes are specifically designed to signal issues that originate from the client's side, such as invalid input data, unauthorized access attempts, or requests for non-existent resources.
  
- **Error Clarification:** Each `4XX` status code provides specific information about the type of client-side error, helping clients quickly identify and rectify the issue.

- **Common `4XX` Codes:**
  - **400 Bad Request**: Indicates that the server cannot process the request due to malformed syntax, invalid input data, or other client-side issues.
  - **401 Unauthorized**: Signals that authentication is required and has failed or is not provided.
  - **403 Forbidden**: Indicates that the client is authenticated but does not have permission to access the requested resource.
  - **404 Not Found**: Used when the requested resource cannot be found on the server.
  - **409 Conflict**: Indicates that the request could not be processed due to a conflict with the current state of the resource.

**Benefits:**
- **Clear Communication:** Using the appropriate `4XX` status code ensures that the client is clearly informed about the specific nature of the error, which helps in understanding and resolving the issue.
- **Enhanced Client-Side Handling:** Precise status codes enable the client to implement more effective error handling and user notifications, improving the overall user experience.

<br><br>


### Consider using an HTTP `429` return code when a client breaks a request rate limit.

// TODO: add description.

```http
// TODO: add example
```

See also: HTTP Methods
<br><br>


### Always use HTTP `5XX` return codes for internal errors, when the issue is on the API's side.

// TODO: add description.

```http
// TODO: add example
```

See also: HTTP Methods
<br><br>


