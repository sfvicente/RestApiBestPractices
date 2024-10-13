# Resources
This section focuses on designing and structuring APIs around well-defined domain entities. It emphasizes using standard HTTP
methods to perform operations on these entities, ensuring a RESTful, consistent, and intuitive API design.

## General Guidelines


### Always model the services around domain entities using the standard HTTP methods as operation indicators
Design your services to revolve around domain entities, using standard HTTP methods to perform operations on those
entities. Avoid modeling service operations as actions; instead, focus on the domain entities that compose the
API model, and apply standard HTTP methods to interact with them.

**Example Request**
```http
GET /api/products/123
```

**Example Response**
```http
HTTP/1.1 200 OK
Content-Type: application/json

{
  "id": 123,
  "name": "Product Name",
  "description": "Product Description",
  "price": 29.99
}
```

**Scenarios**
- **CRUD Operations**: Use standard HTTP methods (GET, POST, PUT, DELETE) to perform Create, Read, Update, and Delete operations on domain entities such as products, users, or orders.
  - **GET**: Retrieve a resource or a collection of resources.
  - **POST**: Create a new resource.
  - **PUT**: Update an existing resource.
  - **DELETE**: Remove a resource.
- **Resource-Based Design**: Focus on entities like "products," "users," or "orders" rather than actions like "createProduct" or "deleteUser." This aligns with REST principles and makes the API more intuitive.
- **Entity Relationships**: Clearly define relationships between entities using appropriate URI structures and standard HTTP methods to navigate and manipulate these relationships.

**Benefits**
- **RESTful Design**: Promotes adherence to REST principles by using standard HTTP methods to operate on resources, resulting in a more predictable and uniform API.
- **Clarity and Consistency**: Enhances clarity and consistency in API design by modeling services around entities and using well-defined methods to interact with them.
- **Simplicity**: Simplifies API usage for clients, as they can rely on standard HTTP methods to perform operations, without needing to understand custom actions or methods.

**Tags:** `domain entities` `HTTP methods` `RESTful design` `API modeling` `resource-based design` `CRUD operations`
<br><br>


### Always design API operations to limit the amount of data returned in a single response

// TODO: add description

```http
// TODO: add examples
```

See also: Paging
<br>


### Consider using a nested URI structure if a sub-resource is only accessible via its parent resource and may not exist without the parent resource
Use a nested URI structure to represent the relationship between parent and sub-resources when the sub-resource cannot
exist independently of the parent resource. This approach helps clearly define the hierarchical relationship and enhances
the readability and organization of the API.

**Example Request**
```http
GET /api/projects/123/tasks/456
```

**Example Response**
```http
HTTP/1.1 200 OK
Content-Type: application/json

{
  "id": 456,
  "projectId": 123,
  "name": "Design the homepage",
  "status": "In Progress"
}
```

**Scenarios**
- **Hierarchical Data**: When dealing with data that has a clear hierarchical relationship, such as projects and their tasks, or orders and their items, where the child resources are inherently tied to their parent resources.
- **Dependent Resources**: When a sub-resource does not make sense or is not useful without the context of its parent resource, such as comments within a blog post or addresses within a user profile.

**Benefits**
- **Clear Relationships**: Clearly indicates the relationship between parent and sub-resources, making the API structure more intuitive and easier to understand.
- **Improved Organization**: Helps in organizing the API endpoints in a logical manner, reflecting the real-world relationships between entities.
- **Scoped Access**: Provides a natural way to scope access to sub-resources, ensuring that operations on sub-resources are appropriately contextualized within the parent resource.

**Tags:** `URI structure` `nested URIs` `hierarchical data` `parent-child relationship` `API design` `resource organization`
<br><br>



## ...