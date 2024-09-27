# Design Principles
Design Principles are the fundamental guidelines that ensure APIs are well-structured, efficient, and easy to use.

## General Guidelines



### Never maintain transient state information between requests
REST APIs use a stateless request model, meaning that each request from a client to the server must contain all the information
needed to understand and process it. The server should not store any state information between requests that is specific to a
user session or transaction.

Maintaining state between requests can lead to inconsistencies, scalability issues, and increased complexity. If state needs to
be maintained, it should be sent explicitly by the client in each request (e.g., using tokens or session identifiers) or persisted
in a database, rather than being kept in the server's memory.

HTTP requests can occur in any order, and the server should be able to handle each one independently, without relying on any prior
or future requests. This ensures better scalability, load distribution, and fault tolerance.

**Example of Stateless Design**:
- When a client logs in, it sends credentials, and the server responds with a token. The client sends this token in each subsequent request to maintain authentication without the server needing to remember the login state.

Maintaining a stateless architecture improves reliability, simplifies debugging, and enables horizontal scaling, as no session
information is tied to a particular server instance.

Additional Tags: State Management
<br><br>


### Design operations to be atomic
Operations should be performed completely or not at all, ensuring that the system remains in a consistent state. An
atomic operation prevents partial updates that could leave the system in an inconsistent or invalid state if a failure
occurs during the operation.

**Examples**:

#### Example for Creating a Resource with Related Entities

When creating a resource that involves related entities, ensure that either all entities are created successfully, or
none are created if an error occurs.

```http
POST /orders
Content-Type: application/json

{
  "customerId": 123,
  "items": [
    {"productId": 1, "quantity": 2},
    {"productId": 2, "quantity": 1}
  ],
  "totalPrice": 150.00
}
```

- **Request**: Attempts to create a new order with related items.

```http
HTTP/1.1 201 Created
Content-Type: application/json
Location: /orders/456

{
  "orderId": 456,
  "customerId": 123,
  "items": [
    {"productId": 1, "quantity": 2},
    {"productId": 2, "quantity": 1}
  ],
  "totalPrice": 150.00,
  "createdAt": "2024-05-15T12:00:00Z",
  "updatedAt": "2024-05-15T12:00:00Z"
}
```

- **Response**: The server responds with a `201 Created` status code and includes the URI of the newly created order. If
any part of the operation fails (e.g., invalid `productId`), the entire operation is rolled back, and no resources are created.

#### Example for Updating a Resource with Multiple Steps

When updating a resource that involves multiple steps, ensure that either all steps are completed successfully, or the
operation is aborted.

```http
PUT /users/123
Content-Type: application/json

{
  "name": "John Doe",
  "email": "john.doe@example.com",
  "address": {
    "street": "123 Main St",
    "city": "Hometown",
    "zip": "12345"
  }
}
```

- **Request**: Attempts to update a user's profile, including their name, email, and address.

```http
HTTP/1.1 200 OK
Content-Type: application/json

{
  "userId": 123,
  "name": "John Doe",
  "email": "john.doe@example.com",
  "address": {
    "street": "123 Main St",
    "city": "Hometown",
    "zip": "12345"
  },
  "updatedAt": "2024-05-15T12:10:00Z"
}
```

- **Response**: The server responds with a `200 OK` status code and includes the updated user information. If any part of
the update fails (e.g., invalid email format), the entire operation is rolled back, and the user's profile remains unchanged.


Designing operations to be atomic is essential for maintaining data integrity and reliability, especially in environments
where multiple clients may be interacting with the API simultaneously.
 
Tags: `atomic operations` `consistency` `data integrity` `rollback` `transaction management` `failure handling` `resource creation` `multi-step updates`
<br><br>



## Consistency Guidelines
<br>


### URLs should be easily read and constructed by users

// TODO: add description

```http
// TODO: add example
```

Additional Tags: URLs
<br><br>


### Always use hyphens to separate words in URLs
When designing URLs for, always use hyphens (`-`) to separate words in order to improve readability and SEO. Hyphens are the
preferred delimiter in URLs, as they are more readable by both humans and search engines. Avoid using underscores (`_`), as
they are less intuitive and can be harder to distinguish in certain fonts.

**Key Points:**
- Hyphens make URLs more legible for users.
- Search engines treat hyphens as word separators, improving searchability.
- Avoid underscores, as they are often not treated as word separators in search engine indexing and are less visually apparent.

**Example:**

```http
GET /api/users/account-settings HTTP/1.1
Host: example.com
```

In this example, `account-settings` is easier to read than `accountsettings` or `account_settings`.

Additional Tags: URLs
<br><br>


### Always follow a consistent URL structure

// TODO: complement description

```http
// TODO: add example
```

Additional Tags: URLs
<br><br>


### Avoid Including Unnecessary Information in URLs

// TODO: complement description

```http
// TODO: add example
```

Additional Tags: URLs
<br><br>


### Always use lowercase letters for URLs

// TODO: complement description

```http
// TODO: add example
```

Additional Tags: URLs
<br><br>


### Always support human-readable identifiers where possible in URLs

// TODO: complement description

```http
// TODO: add example
```

Additional Tags: URLs
<br><br>

