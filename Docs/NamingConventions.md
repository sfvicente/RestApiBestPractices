# Naming Conventions


## General
<br>


### Use nouns to represent resources.
Resources should be represented using nouns to ensure clarity, consistency, and adherence to REST principles.

Using nouns to represent resources offers the following advantages:
- **Semantic Clarity**: Nouns inherently describe entities or objects, making the API endpoints more semantically meaningful.
- **Consistency**: Uniformly using nouns across API endpoints maintains a predictable structure, simplifying API navigation.
- **REST Compliance**: Aligns with the REST architectural style, which emphasizes resource-based interactions.

**Endpoint for User Collection**:
```http
GET /api/users HTTP/1.1
```

**Endpoint for Individual User Resource**:
```http
GET /api/users/{id} HTTP/1.1
```

<sub>See also: Resources</sub>
<br><br>


### Resource names should be pluralized.
Resource names should generally be pluralized to reflect collections of resources. 

Pluralizing resource names offers several benefits:
- **Consistency**: Pluralizing resource names creates a uniform naming convention across API endpoints, enhancing predictability and ease of use.
- **Semantic Clarity**: Plural nouns inherently indicate collections of resources, making the API endpoints more descriptive and intuitive.
- **REST Compliance**: Pluralizing resource names aligns with the standard practice of using plural nouns for representing resource collections in REST APIs.

**Endpoint for Products Collection**:
```http
GET /api/products HTTP/1.1
```

**Endpoint for Individual Product Resource**:
```http
GET /api/products/{id} HTTP/1.1
```

**Tags:** `resources` `resource naming` `pluralized names` `naming conventions` `REST compliance` `collections`
<br><br>


### Forward slashes should be used to indicate hierarchical relationships.
Use forward slashes (/) in your URL paths to represent hierarchical relationships between resources. This practice
enhances the clarity and structure of your API, making it more intuitive and easier to navigate. 

**Example Requests:**
- **Collection of Orders for a Specific Customer**:
    ```http
    GET /api/customers/{customerId}/orders
    ```
- **Specific Order for a Specific Customer**:
    ```http
    GET /api/customers/{customerId}/orders/{orderId}
    ```

**Benefits:**
- **Clarity**: Forward slashes clearly denote parent-child relationships, making it easier to understand how resources are related.
- **Organization**: This structure helps to logically organize resources, reflecting their natural relationships.
- **RESTful Design**: Using hierarchical paths aligns with RESTful principles, promoting a consistent and predictable API design.

**Tags:** `resources` `resource organization` `hierarchical relationships` `URL structure`
<br><br>


### For path segments, prefer the use of lowercase words.

// TODO: add description

```http
// TODO: add example
```

// TODO: complement description

[RFC 3986](https://www.ietf.org/rfc/rfc3986.txt) states that URIs are case-sensitive with the exception of the scheme and host elements.

```http
// TODO: add example
```

See also: Path Segments
<br><br>


### For path segments, prefer the use of words separated with hyphens.
When designing API paths, use hyphens to separate words within path segments. This practice improves readability
and consistency, making it easier for developers to understand and use the API.

**Example Requests:**
- **Product Categories**:
    ```http
    GET /api/product-categories
    ```
- **Customer Orders**:
    ```http
    GET /api/customer-orders
    ```

**Benefits:**
- **Readability**: Hyphens improve the readability of URLs by clearly separating words.
- **SEO Friendly**: Hyphens are preferred in URLs for search engine optimization, as they are more easily interpreted by search engines.
- **Consistency**: Using hyphens consistently across your API ensures a uniform and predictable URL structure.

**Tags:** `path segments` `URL structure` `hyphens` `readability` `consistency` `SEO friendly`
<br><br>


### For query parameters, prefer the use of snake case.

// TODO: add description

```http
// TODO: add example
```

// TODO: complement description

```http
// TODO: add example
```

Additional Tags: Query Parameters
<br><br>


### Do not specify paths with duplicate slashes.

// TODO: add description

```http
// TODO: add example
```

// TODO: complement description

```http
// TODO: add example
```

<br><br>


### Do not specify paths with trailing slashes.
One of the reasons is that adding a trailing slash provides no semantic value.

// TODO: complement description

```http
// TODO: add example
```

// TODO: complement description

```http
// TODO: add example
```

<br><br>


### Do not specify or use path variables with empty string values.

// TODO: add description

```http
// TODO: add example
```

// TODO: complement description

```http
// TODO: add example
```

<br><br>


### Query parameters should use conventional naming.

// TODO: add description

```http
// TODO: add example
```

// TODO: complement description

```http
// TODO: add example
```

See also: Query Parameters
<br><br>

