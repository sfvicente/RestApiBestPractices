# Versioning
The **Versioning** section provides strategies for managing changes to APIs over time without disrupting existing
clients. It includes guidelines for version negotiation, maintaining backward compatibility, and adopting best
practices to handle breaking changes effectively while ensuring a smooth evolution of services.

## General
<br>


### Always increment the version number of services in response to any breaking application change
When a breaking change is introduced to an API, incrementing the version number ensures backward compatibility and allows
clients to continue using previous versions without disruption. This practice provides a clear separation between incompatible
versions, enabling smooth transitions and effective lifecycle management.

- Use semantic versioning (`v1`, `v2`, etc.) in the API URL or headers for clear identification of versions.
- Treat changes to the data structure, endpoint behaviour, or error formats as breaking changes requiring a version increment.
- Maintain documentation for all active versions to support clients still using older versions.

**Client Request to v1**

```http
GET /api/v1/products/123
```

**Server Response from v1**

```http
HTTP/1.1 200 OK
Content-Type: application/json

{
  "id": 123,
  "name": "Product A",
  "price": 29.99
}
```

**Client Request to v2 (Breaking Change Introduced)**

```http
GET /api/v2/products/123
```

**Server Response from v2**

```http
HTTP/1.1 200 OK
Content-Type: application/json

{
  "productId": 123,
  "productName": "Product A",
  "cost": 29.99,
  "currency": "USD"
}
```

**Scenarios**
- **Structural Changes:** Renaming fields or changing the data format (e.g., `price` becomes `cost`).
- **Endpoint Changes:** Modifying or removing endpoints (e.g., merging `/products` and `/inventory` into `/items`).
- **Behavioural Changes:** Altering how an endpoint processes requests or handles errors.

**Tags**: versioning, breaking changes, API lifecycle, backward compatibility
<br><br>


### Consider incrementing the version number of services in response to nonbreaking changes
Incrementing the version number for non-breaking changes can help clients differentiate between API versions while
ensuring they always have access to the latest features. Although not always mandatory, this practice can provide
clarity and transparency, especially when introducing enhancements or optional fields.

- **Use Minor or Patch Versions**: Increment the minor (e.g., `v1.1`) or patch version (e.g., `v1.0.1`) to signal non-breaking updates, such as added fields, new optional parameters, or improved functionality.  
- **Ensure Backward Compatibility**: Guarantee that existing clients can continue using the API without modifications after a version increment.  
- **Communicate Updates Clearly**: Use documentation and changelogs to inform clients about the enhancements in the new version.  

**Client Request to Updated API**

```http
GET /api/products
Accept: application/vnd.myapi.v1.1+json
```

**Server Response with Additional Non-Breaking Field**

```http
HTTP/1.1 200 OK
Content-Type: application/vnd.myapi.v1.1+json

[
  {
    "id": 123,
    "name": "Product A",
    "price": 29.99,
    "discount": 5.00
  }
]
```

**Scenarios**  
- **Adding Fields**: Introduce optional response fields without impacting existing clients.  
- **Enhanced Query Options**: Provide new optional query parameters to extend search or filtering capabilities.  
- **Improved Functionality**: Optimize existing endpoints or add non-disruptive features for better usability.  

Incrementing the version number for non-breaking changes ensures clarity in version history and smooth adoption of enhancements
while maintaining backward compatibility.

**Tags**: API versioning, minor updates, backward compatibility, REST best practices
<br><br>


### Consider incrementing the version number to new major version in response to a future deprecation of services

By increasing the major version, it notifies clients that services will be deprecated and there will be no future support.

// TODO: complement description

```http
// TODO: add example
```

// TODO: complement description

```http
// TODO: add example
```

<br><br>


### Always increment the version number of services when removing operations
Removing a service operation is considered a breaking change because clients relying on the removed
operation will encounter failures. Incrementing the version number ensures clear communication of these
changes to clients and enables them to adapt their integrations accordingly.

- **Treat Removal as a Breaking Change**: Any removal of an operation from a service constitutes a significant change that necessitates versioning.  
- **Increment the Version Number**: Update the version number to indicate the new state of the API and ensure backward compatibility is not implied.  
- **Communicate Clearly**: Notify clients about the removal in advance, providing a timeline and alternative approaches, if available.  

**Example**

**Version 1: Operation Available**

```http
GET /api/v1/orders/123
```

**Response**

```json
{
  "id": 123,
  "status": "shipped",
  "total": 49.99
}
```

**Version 2: Operation Removed**

```http
GET /api/v2/orders/123
```

**Response**

```http
HTTP/1.1 404 Not Found
Content-Type: application/json

{
  "error": "Not Found",
  "message": "The requested operation is no longer supported in this version."
}
```

**Scenarios**  
- **Deprecated Operations**: Before removing an operation, mark it as deprecated in prior versions, and include clear warnings in the API documentation.  
- **Client Updates**: Allow clients adequate time to transition to the updated API version.  
- **Backward Compatibility**: Retain the older API version for a defined period to avoid disrupting existing clients.  

**Cautions**  
- **Breaking Client Applications**: Removing operations without clear communication and proper versioning can lead to failed integrations.  
- **Versioning Overhead**: Frequent breaking changes can complicate version management and increase client maintenance costs.  

By incrementing the version number when removing operations, you ensure transparency and maintain trust with API consumers, while safeguarding against unintended disruptions.

**Tags**: versioning, breaking changes, service evolution, client communication, API lifecycle management
<br><br>


### Always increment the version number of services when renaming operations

Renaming service operations is a breaking change.

// TODO: complement description

```http
// TODO: add example
```

// TODO: complement description

```http
// TODO: add example
```

<br><br>


### Always increment the version number of services when removing operation parameters

Removing service operation parameters is a breaking change.

// TODO: complement description

```http
// TODO: add example
```

// TODO: complement description

```http
// TODO: add example
```

<br><br>


### Always increment the version number of services when renaming operation parameters

Renaming a service operation parameters is a breaking change.

// TODO: complement description

```http
// TODO: add example
```

// TODO: complement description

```http
// TODO: add example
```

<br><br>


### Always increment the version number of services when there are changes in the behavior of an existing service operations

A change in the behavior of existing service operations is a breaking change.

// TODO: complement description

```http
// TODO: add example
```

// TODO: complement description

```http
// TODO: add example
```

<br><br>


### Always increment the version number of services when there are changes in error codes of existing service operations

A change in error codes of existing service operations is a breaking change.

// TODO: complement description

```http
// TODO: add example
```

// TODO: complement description

```http
// TODO: add example
```

<br><br>


### Always increment the version number of services when there are changes in fault contracts of existing service operations

A change in fault contracts of existing service operations is a breaking change.

// TODO: complement description

```http
// TODO: add example
```

// TODO: complement description

```http
// TODO: add example
```

<br><br>


### Avoid using URI based versioning
URI-based versioning involves embedding the version number directly in the API's path (e.g., `/api/v1/resource`). While
simple to implement, this approach introduces several challenges in API maintenance, client-server decoupling, and
scalability. It often results in tighter coupling between components and more complex release management.

- **Promote Header-Based Versioning**: Use headers (e.g., `Accept`) for version negotiation to decouple versioning from resource identifiers and simplify URI structures.  
- **Avoid Hardcoding Versions**: Avoid locking version numbers into the URI structure, as this can lead to redundancy and confusion when maintaining multiple versions.  
- **Ensure Backward Compatibility**: Use strategies that allow incremental changes without requiring constant updates to resource paths.

**Client Request with URI-Based Versioning**

```http
GET /api/v1/products/123
```

**Client Request with Header-Based Versioning**

```http
GET /api/products/123
Accept: application/vnd.myapi.v1+json
```

**Server Response**

```http
HTTP/1.1 200 OK
Content-Type: application/vnd.myapi.v1+json

{
  "id": 123,
  "name": "Product A",
  "price": 29.99
}
```

**Scenarios**
- **Multiple Coexisting Versions**: URI-based versioning requires maintaining distinct endpoints for each version, complicating routing logic and documentation.  
- **Client Migration Challenges**: Changes to URI paths force clients to update hardcoded dependencies, increasing the risk of errors.  
- **Loss of Resource Identity**: Embedding versions in URIs reduces the clarity of resource identification, especially for dynamic linking and hypermedia APIs.

Avoiding URI-based versioning enhances flexibility and consistency, enabling APIs to evolve seamlessly while maintaining a clean and predictable URI structure.

**Tags**: API versioning, URI design, backward compatibility, header-based versioning, REST best practices  
<br><br>


### Prefer the use of media type versioning

// TODO: add description

```http
// TODO: add example
```

// TODO: complement description

```http
// TODO: add example
```

<br><br>