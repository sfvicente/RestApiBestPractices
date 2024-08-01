# Resources


## General


### Model the services around domain entities using the standard HTTP methods as operation indicators.

Do not model service operations as actions. Instead, identify the domain entities that are the components of the API model 
and use the standard HTTP methods to perform the operations on those entities.

For example, do not use the following operation:

// TODO: complement description

```http
// TODO: add examples
```

// TODO: add description

```http
// TODO: add examples
```

See also: HTTP Methods
<br>


### Design the API to limit the amount of data returned by any single request.

// TODO: add description

```http
// TODO: add examples
```

See also: Paging
<br>


### Consider using a nested URI structure if a sub-resource is only accessible via its parent resource and may not exist without the parent resource.
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