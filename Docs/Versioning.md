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

// TODO: add description

```http
// TODO: add example
```

// TODO: complement description

```http
// TODO: add example
```

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

Removing a service operation is a breaking change.

// TODO: complement description

```http
// TODO: add example
```

// TODO: complement description

```http
// TODO: add example
```

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