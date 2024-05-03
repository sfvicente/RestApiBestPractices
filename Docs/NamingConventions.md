# Naming Conventions


## General
<br>


### Represent Resources with Nouns.

Resources should be represented using nouns to ensure clarity, consistency, and adherence to REST principles.

Using nouns to represent resources offers the following advantages:
- **Semantic Clarity**: Nouns inherently describe entities or objects, making the API endpoints more semantically meaningful.
- **Consistency**: Uniformly using nouns across API endpoints maintains a predictable structure, simplifying API navigation.
- **REST Compliance**: Aligns with the REST architectural style, which emphasizes resource-based interactions.

**Endpoint for User Collection (plural noun)**:
```http
GET /api/users HTTP/1.1
```

**Endpoint for Individual User Resource (singular noun)**:
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

<sub>See also: Resources</sub>
<br><br>


### Forward slashes should be used to indicate hierarchical relationships.

// TODO: add description

```http
// TODO: add example
```

// TODO: complement description

```http
// TODO: add example
```

See also: Path Segments
<br><br>


### For path segments, prefer the use of lowercase words.

// TODO: add description

```http
// TODO: add example
```

// TODO: complement description

[RFC 3986](https://www.ietf.org/rfc/rfc3986.txt) states that URIs are case-sensitive with the exceptopn of the scheme and host elements.

```http
// TODO: add example
```

See also: Path Segments
<br><br>


### For path segments, prefer the use of words separated with hyphens.

// TODO: add description

```http
GET /payment-methods
```

// TODO: complement description

```http
// TODO: add example
```

See also: Path Segments
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

