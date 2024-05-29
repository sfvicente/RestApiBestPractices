# Introduction to REST

In software engineering, REST (Representational State Transfer) is an architectural style for designing networked
applications. It relies on a stateless, client-server communication protocol, typically HTTP. Here are the key 
principles and characteristics that define REST:

1. **Statelessness**: Each client request to the server must contain all the information needed to understand and process the request. The server does not store any state about the client session on its end. This simplifies the server design and improves scalability since the server does not need to manage or track session state.

2. **Client-Server Architecture**: The system is divided into clients and servers. Clients are responsible for the user interface and user experience, while servers manage data storage and business logic. This separation allows for the independent evolution of client and server components.

3. **Uniform Interface**: RESTful systems adhere to a uniform interface between components, which simplifies and decouples the architecture. The uniform interface is typically based on:
   - **Resource Identification**: Each resource (data object or service) is identified by a unique URI (Uniform Resource Identifier).
   - **Resource Manipulation through Representations**: Clients interact with resources using representations, such as JSON or XML, and can manipulate these resources using standard HTTP methods (GET, POST, PUT, DELETE).
   - **Self-descriptive Messages**: Each message contains enough information to describe how to process it. For example, metadata about the message can be included in HTTP headers.
   - **Hypermedia as the Engine of Application State (HATEOAS)**: Clients interact with the application entirely through hypermedia provided dynamically by application servers. This means that the server provides information on what actions are available at any point in time.

4. **Layered System**: A RESTful system may consist of multiple layers, with each layer providing different functions. For example, there might be intermediaries like proxies or gateways between the client and server, which can help with load balancing, security, and caching. These layers are transparent to the client.

5. **Cacheability**: Responses from the server should be explicitly marked as cacheable or non-cacheable to improve performance. If a response is cacheable, clients or intermediaries can reuse the response data for subsequent requests, reducing the need for redundant processing and improving efficiency.

6. **Code on Demand (Optional)**: Servers can extend the functionality of a client by transferring executable code, such as JavaScript. This is an optional constraint and is not required for RESTful services.

REST is a lightweight and flexible approach to designing web services that can efficiently handle the complexity and scale of modern web applications.
<br>

