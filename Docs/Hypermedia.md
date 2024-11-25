# Hypermedia
Hypermedia is a key feature of REST that enables APIs to guide clients dynamically by including links, actions, and
metadata in responses. It allows clients to navigate resources, perform operations, and discover related endpoints
without relying solely on hardcoded URLs or external documentation. By embedding contextual links and controls, 
hypermedia ensures flexibility, enhances discoverability, and promotes decoupling between client and server.

## General

...


## ...

## Use HATEOAS to Provide Navigation Links in Responses

## Include Self Links (`_self`) to Identify Resource Locations
Providing a `_self` link in API responses helps clients identify the canonical URL for the returned resource. This
ensures clarity, supports hypermedia-driven interactions, and allows clients to make further requests to the
resource without relying on hardcoded paths.

- **Always Include a `_self` Link**: Embed a `_self` link in every resource representation to indicate the resource's location.  
- **Use Absolute URLs When Possible**: Include full URLs in `_self` links to simplify client-side construction and avoid ambiguity.  
- **Keep Links Up-to-Date**: Ensure `_self` links accurately reflect the current location or state of the resource, even after updates or moves.  
- **Support Discoverability**: Use `_self` links to enable clients to dynamically discover and interact with resources without prior knowledge of the API structure.  

**Client Request**

```http
GET /api/products/123
```

**Server Response with `_self` Link**

```http
HTTP/1.1 200 OK
Content-Type: application/json

{
  "id": 123,
  "name": "Product A",
  "price": 29.99,
  "_links": {
    "self": "/api/products/123"
  }
}
```

**Scenarios**  
- **Resource Identification**: Use `_self` links to provide the exact URL for accessing or modifying the resource.  
- **Dynamic APIs**: In APIs with frequently changing structures, `_self` links allow clients to adapt to changes without hardcoding paths.  
- **Inter-resource Linking**: Include `_self` links when embedding related resources to clarify relationships and navigation paths.

Adding `_self` links in API responses ensures that resource locations are explicit and easily accessible, enhancing usability and maintainability.

**Tags**: hypermedia, `_self` link, resource location, REST discoverability, API usability
<br><br>


## Provide Contextual Links for Related Resources

## Use Link Relations (e.g., `rel`) to Describe Link Purposes
Link relations (`rel` attributes) describe the purpose of a hyperlink in an API response, providing clients with
semantic context about the relationship between resources. By using standard or custom link relations, APIs
become more self-explanatory, enabling better navigation and automation.

- Include a `rel` attribute in all hypermedia links to indicate their purpose (e.g., `self`, `next`, `prev`, `related`).  
- Use standard link relation values defined by the [IANA Link Relations Registry](https://www.iana.org/assignments/link-relations/link-relations.xhtml) when applicable.  
- For domain-specific use cases, define and document custom `rel` values to maintain clarity.

**Client Request**

```http
GET /api/products/123
```

**Server Response**

```http
HTTP/1.1 200 OK
Content-Type: application/json

{
  "id": 123,
  "name": "Product A",
  "links": [
    {
      "rel": "self",
      "href": "/api/products/123"
    },
    {
      "rel": "related",
      "href": "/api/categories/45"
    },
    {
      "rel": "reviews",
      "href": "/api/products/123/reviews"
    }
  ]
}
```

**Scenarios**
- **Self-Referential Links:** Include a `self` link for the resource being returned.  
- **Pagination:** Use `next` and `prev` relations to guide clients through paginated collections.  
- **Related Resources:** Provide links to associated resources, such as categories or reviews, with clear `rel` descriptions.  

Using `rel` attributes standardizes link purpose across APIs, improving usability, discoverability, and client interaction.

**Tags**: link relations, hypermedia, HATEOAS, API navigation, semantic links  
<br><br>


## Support Pagination with Hypermedia Controls (e.g., `next`, `prev`)
Hypermedia controls for pagination, such as `next` and `prev` links, simplify navigating through large datasets
by embedding navigation metadata directly in the response. This approach enhances usability and ensures clients
can dynamically follow links without hardcoding pagination logic.

- **Include `next` and `prev` Links**: Embed `next` and `prev` URLs in the response body to guide clients through paginated results.  
- **Use `self` Links for Context**: Provide a `self` link to identify the current page and its parameters.  
- **Return Metadata**: Include additional pagination metadata (e.g., `totalItems`, `page`, `pageSize`) to help clients display navigation controls.  
- **Ensure Consistency**: Use the same pagination scheme across all endpoints to maintain predictability.

**Client Request**

```http
GET /api/products?page=2&pageSize=5
```

**Server Response with Hypermedia Controls**

```http
HTTP/1.1 200 OK
Content-Type: application/json

{
  "page": 2,
  "pageSize": 5,
  "totalItems": 50,
  "totalPages": 10,
  "items": [
    { "id": 6, "name": "Product F", "price": 19.99 },
    { "id": 7, "name": "Product G", "price": 29.99 },
    { "id": 8, "name": "Product H", "price": 39.99 },
    { "id": 9, "name": "Product I", "price": 49.99 },
    { "id": 10, "name": "Product J", "price": 59.99 }
  ],
  "_links": {
    "self": "/api/products?page=2&pageSize=5",
    "next": "/api/products?page=3&pageSize=5",
    "prev": "/api/products?page=1&pageSize=5"
  }
}
```

**Scenarios**  
- **Paged Lists**: Use hypermedia controls for APIs returning large datasets (e.g., product lists, user directories).  
- **Dynamic Navigation**: Allow clients to follow links without prior knowledge of pagination logic.  
- **Flexible Clients**: Enhance client implementations by providing all necessary metadata for navigation and display.

Embedding hypermedia controls in pagination ensures intuitive navigation and simplifies client implementation while adhering to REST principles.

**Tags**: pagination, hypermedia, REST navigation, page links, usability
<br><br>


## Provide Forms or Templates for Actionable Resources

## Document Hypermedia Controls and Link Relations Clearly

## Embed Links for Optional Operations Based on User Roles or State
Including links for optional operations, tailored to user roles or the resource state, enables clients to discover
context-sensitive actions dynamically. This approach adheres to HATEOAS principles, simplifying API interactions
and reducing hardcoded logic on the client side.

- **Role-Specific Links**: Provide links for operations that are available only to specific user roles (e.g., admin-only actions).  
- **State-Dependent Links**: Embed links based on the resource's current state (e.g., a `complete` action for an order that is still pending).  
- **Clear Link Documentation**: Use descriptive `rel` attributes to clarify the purpose of each link.  
- **Omit Unavailable Links**: Avoid including links for actions the client cannot perform, reducing confusion and error-prone requests.  

**Client Request**

```http
GET /api/orders/456
```

**Server Response with Role and State-Based Links**

```http
HTTP/1.1 200 OK
Content-Type: application/json

{
  "id": 456,
  "status": "pending",
  "items": [
    { "id": 1, "name": "Widget A", "quantity": 2 },
    { "id": 2, "name": "Widget B", "quantity": 1 }
  ],
  "_links": {
    "self": "/api/orders/456",
    "approve": "/api/orders/456/approve",
    "cancel": "/api/orders/456/cancel"
  }
}
```

In this example:  
- The `approve` link is available because the order is `pending`.  
- A `ship` link might appear only after the order is approved.

**Scenarios**  
- **Role-Based Operations**: Admins may see links to delete or archive resources, while standard users see only view or edit links.  
- **State-Specific Actions**: Dynamic links based on resource states guide the client to permissible actions, such as canceling an active order or completing a draft.  
- **Dynamic Permission Handling**: Links reflect real-time access permissions, ensuring client-side logic aligns with server-side policies.  

Embedding context-sensitive links simplifies client integration, minimizes errors, and creates a dynamic, adaptive API experience.

**Tags**: hypermedia, optional links, user roles, resource state, dynamic actions, HATEOAS principles
<br><br>


## Design Consistent Hypermedia Responses Across Endpoints

## Use Standard Media Types for Hypermedia (e.g., HAL, JSON:API)
