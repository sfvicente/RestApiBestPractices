# Sorting


## General
<br>


### Consider allowing clients to specify sort order in search results
Enabling clients to specify the sort order of search results can significantly enhance the usability and flexibility
of an API. By providing options for sorting, clients can retrieve data in a manner that best suits their needs, making
it easier to find relevant information quickly.

When clients can dictate the sorting criteria, they can prioritize the data that is most important to them, whether
it’s by relevance, date, name, or any other relevant attribute. This feature can improve user satisfaction and streamline
the development process by reducing the need for additional post-processing on the client side.

**Key Points:**
- **Enhances user experience**: Allowing sort order customization can lead to a more intuitive and efficient interaction with the API.
- **Supports diverse use cases**: Different clients may have varying requirements for how they want data presented.
- **Improves performance**: Sorting at the server level can reduce the amount of data processing needed on the client side.

**Example of a search request with sort order:**
```http
GET /api/v1/products?sort=price_desc
```

In this example, the client requests a list of products sorted by price in descending order. By supporting such query parameters,
the API becomes more flexible and tailored to user preferences.
<br><br>


### Consider allowing results of a collection query to be sorted based on property values.

// TODO: add description

```http
// TODO: add example
```

// TODO: complement description

```http
// TODO: add example
```

<br><br>


### Always sort `null` values as less than values which are not `null`.

// TODO: add description

```http
// TODO: add example
```

// TODO: complement description

```http
// TODO: add example
```

<br><br>


### Always allow sorting to be combined with the filtering mechanism.

// TODO: add description

```http
// TODO: add example
```

// TODO: complement description

```http
// TODO: add example
```

See also: Filtering
<br><br>



## ...