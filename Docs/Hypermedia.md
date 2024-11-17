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

## Provide Forms or Templates for Actionable Resources

## Document Hypermedia Controls and Link Relations Clearly

## Embed Links for Optional Operations Based on User Roles or State

## Design Consistent Hypermedia Responses Across Endpoints

## Use Standard Media Types for Hypermedia (e.g., HAL, JSON:API)
