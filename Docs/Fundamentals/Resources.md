# Resources

Resources are the fundamental abstractions in RESTful architectures, and they are typically identified by URIs (Uniform Resource Identifiers).

A resource is a conceptual mapping to a set of entities, data, or functionality that can be accessed, manipulated, and
linked together using standard HTTP methods and URIs. Each resource is uniquely identified by a URI.

- **Examples of Resources**:
  - An individual user profile (`/users/johndoe`)
  - A collection of articles (`/articles`)
  - A specific article (`/articles/123`)
  - A product in an e-commerce system (`/products/789`)

- **Characteristics**:
  - **State**: A resource has state, which represents the current information or data associated with that resource.
  - **Identity**: A resource has a unique identifier (URI) that distinguishes it from other resources.
  - **Representation**: Resources can have different representations (e.g., JSON, XML) based on the client's needs and preferences.

- **Operations on Resources**:
  - **HTTP Methods**: RESTful APIs use standard HTTP methods (GET, POST, PUT, DELETE, etc.) to perform operations on resources:
    - `GET`: Retrieve a representation of the resource.
    - `POST`: Create a new resource.
    - `PUT` or `PATCH`: Update an existing resource.
    - `DELETE`: Delete a resource.

- **Resource Relationships**: Resources can be related to each other. For example:
  - A user resource may be associated with multiple articles they've authored.
  - An order resource may be linked to the customer who placed the order.

- **Uniform Interface**: Resources in REST APIs are manipulated through a uniform interface, which consists of standard methods and representations. This simplifies the API design and promotes interoperability.