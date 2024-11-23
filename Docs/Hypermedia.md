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

## Design Consistent Hypermedia Responses Across Endpoints

## Use Standard Media Types for Hypermedia (e.g., HAL, JSON:API)
