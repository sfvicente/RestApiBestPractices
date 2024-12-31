# Hypermedia
Hypermedia is a key feature of REST that enables APIs to guide clients dynamically by including links, actions, and
metadata in responses. It allows clients to navigate resources, perform operations, and discover related endpoints
without relying solely on hardcoded URLs or external documentation. By embedding contextual links and controls, 
hypermedia ensures flexibility, enhances discoverability, and promotes decoupling between client and server.

## General

...


## ...

## Use HATEOAS to Provide Navigation Links in Responses
Hypermedia as the Engine of Application State (HATEOAS) is a REST principle that enhances API interactions
by embedding navigation links in responses. These links guide clients through the API dynamically, reducing
reliance on static documentation and hardcoded paths.  

- **Include Hypermedia Links**: Add links that point to related resources or actions the client can perform, such as `self`, `next`, `prev`, `create`, or `update`.  
- **Use Standard Link Relations**: Adopt well-defined `rel` attributes (e.g., `self`, `next`, `prev`, `edit`, `delete`) to describe the purpose of each link.  
- **Dynamic Discovery**: Enable clients to navigate through your API dynamically based on the provided links rather than predefined assumptions.  

**Examples**  

1. **Correct Usage**  
```json
{
  "id": 123,
  "name": "John Doe",
  "email": "john.doe@example.com",
  "links": [
    { "rel": "self", "href": "/users/123" },
    { "rel": "update", "href": "/users/123/edit" },
    { "rel": "delete", "href": "/users/123" }
  ]
}
```

2. **Incorrect Usage**  
```json
{
  "id": 123,
  "name": "John Doe",
  "email": "john.doe@example.com"
}
```

**Scenarios**  
- **Resource Navigation**: Provide links for pagination (e.g., `next`, `prev`, `first`, `last`) in collection responses.  
- **Action Availability**: Include links for actions like updating, deleting, or transitioning the state of a resource.  
- **API Evolution**: Add new features or endpoints without breaking clients, as they dynamically discover available links.  

**Benefits**  
- **Improved Usability**: Reduces the need for static client-side knowledge of resource paths.  
- **Dynamic Exploration**: Allows clients to adapt to API changes by following links rather than relying on hardcoded URIs.  
- **Simplified Documentation**: Reduces the need for detailed path specifications in API documentation.  

**Cautions**  
- **Consistency in Links**: Ensure all endpoints providing similar functionality include the same relevant links.  
- **Avoid Overloading Links**: Include only meaningful and actionable links to avoid overwhelming clients.  
- **Versioning Considerations**: Adapt links when introducing new API versions to maintain functionality.  

**Tags**: hateoas, hypermedia links, api navigation, response design, restful principles.
<br><br>


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
Contextual links in hypermedia responses enhance the usability and navigability of APIs by including links
to relevant resources. These links help clients discover and interact with related data or operations without
relying on hardcoded logic or external documentation.  

- **Identify Relevant Relationships**: Include links to resources that have logical or functional connections to the current resource, such as parent, child, or sibling relationships.  
- **Use Meaningful `rel` Attributes**: Clearly describe the purpose of each link using standard or custom `rel` attributes (e.g., `related`, `parent`, `child`, `collection`).  
- **Include Links Based on Context**: Dynamically determine which links to include based on the resource's state, user roles, or other contextual factors.  

**Examples**  

1. **Correct Usage**  
```json
{
  "id": 45,
  "title": "API Design Principles",
  "author": "Jane Doe",
  "links": [
    { "rel": "self", "href": "/articles/45" },
    { "rel": "author", "href": "/users/12" },
    { "rel": "related", "href": "/categories/api-design" }
  ]
}
```

2. **Incorrect Usage**  
```json
{
  "id": 45,
  "title": "API Design Principles",
  "author": "Jane Doe"
}
```

**Scenarios**  
- **Parent-Child Relationships**: A blog post response should link to its author and category.  
- **Resource Aggregation**: A collection response should link to individual resources within the collection.  
- **Cross-Entity Connections**: A user profile should link to their orders, reviews, or related activity.  

**Benefits**  
- **Discoverability**: Clients can discover related resources without additional requests or assumptions.  
- **Dynamic Adaptability**: Allows APIs to evolve while minimizing disruption, as clients dynamically follow provided links.  
- **Improved Efficiency**: Reduces the need for separate API calls to retrieve relationships.  

**Cautions**  
- **Avoid Redundancy**: Do not include links that can be trivially derived or are already part of the resource path.  
- **Consistent Implementation**: Ensure similar resources consistently provide the same contextual links.  
- **Scalability**: Balance the number of links to avoid overly large responses that degrade performance.  

**Tags**: hypermedia, contextual links, related resources, discoverability, restful design.  
<br><br>


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
Hypermedia responses enhance API usability by embedding links within responses, guiding clients on available actions
and navigation paths. Consistency in hypermedia design ensures predictable structures across endpoints, fostering seamless
integration and reducing client-side implementation complexity.  

**Key Hypermedia Concepts**  
- **HATEOAS (Hypermedia as the Engine of Application State)**: Links within responses direct clients to discover and perform operations dynamically, reducing reliance on hardcoded URLs.  
- **Self-Descriptive Responses**: Each response includes enough context to guide the client’s next steps.  
- **Link Relations**: Define the purpose of each link using standard or custom relation types (e.g., `self`, `next`, `previous`).  

**Example: Consistent Hypermedia Response**  
```json
{
  "id": 123,
  "name": "example",
  "status": "active",
  "links": [
    { "rel": "self", "href": "/resources/123" },
    { "rel": "update", "href": "/resources/123", "method": "PATCH" },
    { "rel": "delete", "href": "/resources/123", "method": "DELETE" }
  ]
}
```  

**Consistency Guidelines**  
1. **Uniform Structure**  
   - Use a standard property name, such as `links`, across all endpoints for hypermedia elements.  
   - Ensure link relations (`rel`) are self-explanatory and align with established standards like [IANA Link Relations](https://www.iana.org/assignments/link-relations/link-relations.xhtml).  

2. **Action Metadata**  
   - Include HTTP methods (`GET`, `POST`, etc.) for each link to clarify supported actions.  
   - Specify required payload structures or query parameters, if applicable.  

3. **Context-Aware Links**  
   - Dynamically generate links based on the resource state. For example:  
     - For inactive resources, omit `update` or `delete` links.  
     - Include `activate` or `retry` links as appropriate.  

**Recommendations**  
- Design hypermedia responses to match the API's domain-specific workflows, guiding clients effectively.  
- Avoid overloading responses with unnecessary links; only include those relevant to the client’s immediate context.  
- Clearly document link relations and their expected behavior in the API specification.  
- Ensure backward compatibility by maintaining consistent hypermedia structures when updating APIs.  

**Benefits of Consistent Hypermedia Design**  
- Reduces hardcoded client logic, enabling better adaptability to API changes.  
- Simplifies navigation and action discovery for client developers.  
- Supports dynamic workflows, especially in APIs with complex relationships and operations.  

By designing consistent hypermedia responses across endpoints, APIs can improve developer experience, enhance adaptability, and ensure smooth client interactions with dynamic and evolving services.  
<br><br>


## Use Standard Media Types for Hypermedia (e.g., HAL, JSON:API)
Adopting standard media types like HAL or JSON:API for hypermedia APIs promotes consistency, interoperability, and
ease of use. These formats define conventions for structuring resources and embedding links, enabling clients to
navigate and interact with APIs effectively.

- **Choose a Standard**: Select a hypermedia format like HAL (Hypertext Application Language) or JSON:API to structure API responses consistently.  
- **Embed Links and Metadata**: Use standard properties (e.g., `_links` in HAL or `links` in JSON:API) to include navigational links and related metadata.  
- **Follow Specification Rules**: Ensure your API adheres strictly to the chosen media type’s specifications for compatibility with libraries and tools.  
- **Simplify Client Development**: Leverage client libraries built for standard media types to reduce implementation complexity and errors.  

**Example Using HAL**

**Client Request**

```http
GET /api/products/123
```

**Server Response in HAL Format**

```http
HTTP/1.1 200 OK
Content-Type: application/hal+json

{
  "id": 123,
  "name": "Product A",
  "price": 29.99,
  "_links": {
    "self": { "href": "/api/products/123" },
    "category": { "href": "/api/categories/456" }
  }
}
```

**Example Using JSON:API**

**Client Request**

```http
GET /api/products/123
```

**Server Response in JSON:API Format**

```http
HTTP/1.1 200 OK
Content-Type: application/vnd.api+json

{
  "data": {
    "type": "products",
    "id": "123",
    "attributes": {
      "name": "Product A",
      "price": 29.99
    },
    "links": {
      "self": "/api/products/123"
    },
    "relationships": {
      "category": {
        "links": {
          "related": "/api/categories/456"
        }
      }
    }
  }
}
```

**Scenarios**  
- **Navigable APIs**: Use standard media types to simplify client navigation across related resources.  
- **Third-Party Integrations**: Ensure compatibility with existing libraries and frameworks built for standard formats.  
- **Reduced Documentation Burden**: Clients familiar with the media type can use your API without needing extensive custom documentation.  

By leveraging standard media types, APIs become more predictable, reusable, and easier to integrate, aligning with industry best practices.

**Tags**: hypermedia, media types, HAL, JSON:API, consistency, interoperability, REST standards
<br><br>