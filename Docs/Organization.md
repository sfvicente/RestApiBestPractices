# Organization


## General Guidelines
<br>


### Avoid generating complex resource URIs.
Keeping resource URIs simple and straightforward enhances usability and maintainability. Complex URIs can lead to confusion
and make it more challenging for users to interact with your API effectively. By adhering to a clear and logical structure,
developers can navigate resources with greater ease.

Avoid requiring resource URIs that exceed the structure of `collection/item/collection`, as overly complicated URIs can result
in increased chances of error and hinder user experience. A well-defined URI structure also facilitates better documentation
and understanding of the API's functionality.

**Key Points:**
- **Use clear hierarchical structures**: Stick to a straightforward path that reflects the relationships between resources.
- **Minimize depth**: Avoid deep nesting of resources in URIs, which can complicate requests and responses.
- **Make it intuitive**: Design URIs that are easy to read and remember, enhancing the developer experience.

**Example of a complex URI:**
```http
GET /api/v1/categories/123/products/456/details/extra-info
```

**Improved simple URI:**
```http
GET /api/v1/categories/123/products/456
```

In the improved example, the URI is simpler and focuses on accessing a specific product within a category, making it easier to understand and work with.
<br><br>




## ...