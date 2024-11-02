# Sorting


## General Guidelines
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


### Consider allowing results of a collection query to be sorted based on property values
To enhance flexibility and user experience, consider enabling clients to sort the results of a collection query based on specific
property values. Allowing sorting by one or more fields (such as name, date, or price) provides users with greater control over the
data returned, making it easier to retrieve and work with the most relevant information.

Supporting sorting can be especially useful in large datasets where users may want to see results in a specific order, such as
alphabetical listings or by recent activity. It's important to provide clear documentation on which fields are available for sorting
and to handle invalid sorting parameters gracefully, returning an appropriate error message if needed.

**Best Practices:**
- Use query parameters to specify the sort field and direction (e.g., ascending or descending).
- Allow sorting on multiple fields if relevant to the data model.
- Ensure the default sort order is logical and predictable.

**Example:**

```http
GET /api/v1/products?sort=price&order=asc HTTP/1.1
Host: example.com
```

In this example, the client requests a list of products sorted by `price` in ascending order, enabling a more tailored response for their needs.

<br><br>


### Always sort `null` values as less than values which are not `null`
To ensure consistent sorting and predictable client responses, always sort `null` values to appear before non-`null`
values in any API results where sorting applies. This practice provides a clear ordering standard and prevents
unexpected results when `null` values are present in the dataset.

**Example Scenario**

```http
GET /api/products?sort=price
```

**Expected Response**

Given products with prices `[null, 5.99, null, 15.49, 7.00]`, the server response would sort the prices with `null` values appearing first:

```http
HTTP/1.1 200 OK
Content-Type: application/json

[
  { "id": 1, "name": "Product A", "price": null },
  { "id": 2, "name": "Product B", "price": null },
  { "id": 3, "name": "Product C", "price": 5.99 },
  { "id": 4, "name": "Product D", "price": 7.00 },
  { "id": 5, "name": "Product E", "price": 15.49 }
]
```

**Benefits**
- **Consistency:** Keeps API responses uniform, regardless of client.
- **Predictability:** Helps clients handle `null` values consistently, especially in ordered or paginated responses.
- **Compatibility:** Commonly aligns with SQL and database sorting defaults, making backend integration straightforward.

**Tags**: sorting, `null` values, ordering
<br><br>


### Always allow sorting to be combined with the filtering mechanism

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