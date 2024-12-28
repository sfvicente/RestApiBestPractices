# Compatibility and Versioning  
This section provides comprehensive guidance for evolving APIs while maintaining a seamless experience for clients. It outlines
strategies to manage versioning effectively, ensuring backward and forward compatibility. By following these practices, you can
introduce new features, handle breaking changes, and negotiate API versions without disrupting existing integrations. This approach
promotes long-term stability, ease of maintenance, and a reliable API experience that fosters adoption and trust.

## General Guidelines
<br>


### Avoid ignoring unknown input fields in the message payload by returning an error with an HTTP 400 status code
To maintain strict validation and ensure the integrity of API requests, avoid silently ignoring unknown input fields in the message
payload. Instead, return a clear error response, such as an HTTP `400 Bad Request` status code, to inform clients that the request
includes invalid or unexpected data. This approach prevents confusion, ensures clients are aware of any incorrect usage, and reinforces
proper use of the API.

By validating payloads and rejecting requests with unknown fields, you can reduce potential security risks, prevent data pollution,
and make the API behavior more predictable and reliable. Clear feedback also helps developers quickly identify mistakes and adjust
their client requests accordingly.

**Key Points:**
- **Enhances clarity and transparency**: Clients are informed of mistakes rather than unknowingly submitting invalid data.
- **Improves security**: Rejecting unknown fields reduces the attack surface by avoiding unanticipated inputs.
- **Reinforces proper API usage**: Ensures clients adhere to the API’s expected schema and structure.

**Example of an invalid request with unknown fields:**
```http
POST /api/v1/users
Content-Type: application/json

{
  "name": "John Doe",
  "email": "john.doe@example.com",
  "age": 30,  // Valid field
  "unexpectedField": "some value"  // Unknown field
}
```

**Response:**
```http
HTTP/1.1 400 Bad Request
Content-Type: application/json

{
  "error": "Unknown field: unexpectedField"
}
```

In this example, the API rejects the request and returns an error message indicating that an unknown field was provided.

Tags: `validation`, `error-handling`, `security`, `http-400-bad-request`, `data-integrity`, `payload-validation`, `client-feedback`, `input-validation`, `schema-compliance`, `error-response`
<br><br>


### Avoid ignoring unknown input fields in the URI by returning an error with an HTTP 400 status code
To ensure that API requests are accurately formed and to prevent unexpected behavior, avoid silently accepting unknown fields
in the URI. Instead, return an HTTP `400 Bad Request` status code to clearly indicate that the request contains invalid or
unexpected parameters. This approach improves clarity and helps clients understand when their requests do not meet the API’s
expected format.

Validating the structure of the URI and rejecting any unknown fields ensures consistency, enhances security, and reduces
potential errors caused by incorrect parameters.

**Key Points:**
- **Promotes consistency**: Ensures that only recognized fields are processed by the API.
- **Improves error detection**: Clients are informed when they provide invalid parameters, helping them correct requests faster.
- **Enhances security**: Prevents the potential misuse of unanticipated or undefined URI fields.

**Example of an invalid request with unknown fields in the URI:**
```http
GET /api/v1/users/123/profile/unexpectedField
```

**Response:**
```http
HTTP/1.1 400 Bad Request
Content-Type: application/json

{
  "error": "Unknown URI field: unexpectedField"
}
```

In this example, the API rejects the request due to the presence of an unrecognized field (`unexpectedField`) in the URI and returns an error message to the client.

Tags: `error-handling`, `http-400`, `uri-validation`, `input-validation`, `client-feedback`, `api-security`, `consistency`, `unknown-fields`
<br><br>










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
Deprecating a service or endpoint is a significant change that can disrupt client applications reliant on the affected
functionality. While the service may remain temporarily available, announcing its deprecation with a planned removal
date warrants careful handling. Incrementing the major version number provides a clear signal to clients that they must
migrate to updated endpoints or services before the deprecation is enforced.  

Service deprecation is often accompanied by the introduction of new or alternative services, necessitating clear
communication to clients about the timeline and steps required for migration.  

**Example: Deprecation Announcement in API Documentation**  
- **Deprecated Service**: `/v1/resource`  
  - **Deprecation Notice**: "This endpoint will be retired on 2025-12-31. Please migrate to `/v2/resource`."  

**New Service**  
- `/v2/resource` (provides equivalent or improved functionality)  

**Recommendations**  
- **Versioning**: Introduce a new major version alongside the announcement of deprecation to mark the availability of alternative endpoints or services.  
- **Communication**: Include a clear deprecation timeline in API documentation, specifying the removal date and migration instructions.  
- **Backward Compatibility**: Maintain the deprecated service in its current state until the removal date, ensuring clients have sufficient time to transition.  
- **Monitoring**: Track usage of the deprecated service to understand client migration progress and provide additional support if necessary.  

By incrementing the version number and planning service deprecation thoughtfully, you minimise disruption to clients and maintain trust in the API’s reliability.  
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
Renaming operation parameters, whether in requests or responses, constitutes a breaking change. This alteration
can disrupt client applications relying on the original parameter names, leading to unexpected failures or
misinterpretations. Incrementing the version number ensures clients are aware of the change and can update their
implementations accordingly.  

Operation parameters are the inputs and outputs that define how a service communicates with clients. Renaming
these parameters, even with a minor adjustment, can break existing integrations by causing issues such as invalid
requests or missing data in responses.  

**Original request example**  
```json
{
  "userId": 123,
  "email": "example@example.com"
}
```  

**Modified request example (breaking change)**  
```json
{
  "user_id": 123,
  "email_address": "example@example.com"
}
```  

**Versioned endpoint examples**  
- `/v1/resource` (uses `userId` and `email`)  
- `/v2/resource` (uses `user_id` and `email_address`)  

**Recommendations**  
- **Versioning**: Increment the major version whenever parameter names are changed, regardless of how minor the adjustment may seem.  
- **Documentation**: Clearly detail parameter name changes in release notes, including a mapping between old and new names to assist clients in updating their requests and responses.  
- **Backward Compatibility**: Maintain support for the old parameter names in the previous version to provide a transition period for clients.  
- **Communication**: Notify clients in advance of planned parameter renaming, offering detailed guidance and example implementations for the new version.  

By versioning changes to parameter names, you safeguard client applications from unexpected disruptions and uphold the integrity of your service’s API.  
<br><br>


### Always increment the version number of services when removing operation parameters
Removing operation parameters is considered a breaking change because it alters the expected interface between the client
and the server. Clients relying on the removed parameters may encounter errors or unexpected behaviour. Incrementing the
version number communicates this change effectively, allowing clients to adapt accordingly.

- **Treat Parameter Removal as a Breaking Change**: Removing parameters changes the API's contract and impacts client integrations.  
- **Increment the Version Number**: Update the version number whenever operation parameters are removed to signal the change explicitly.  
- **Communicate in Advance**: Provide clear deprecation warnings and migration guidance for clients before removing parameters.  

**Example**

**Version 1: Parameter Available**

```http
GET /api/v1/orders?includeItems=true
```

**Response**

```json
{
  "id": 123,
  "status": "shipped",
  "items": [
    { "name": "Book", "quantity": 1 },
    { "name": "Pen", "quantity": 3 }
  ]
}
```

**Version 2: Parameter Removed**

```http
GET /api/v2/orders
```

**Response**

```json
{
  "id": 123,
  "status": "shipped"
}
```

Here, the `includeItems` parameter was removed, and the response no longer includes the `items` array.

**Scenarios**  
- **Deprecated Parameters**: Before removing a parameter, mark it as deprecated in the earlier version and provide clear documentation of the upcoming change.  
- **Client Adaptation**: Allow sufficient time for clients to transition to the updated API version.  
- **Backward Compatibility**: Retain the older version of the API for a defined period to prevent disruptions for existing clients.  

**Cautions**  
- **Client Disruption**: Removing parameters without versioning or communication can break existing integrations.  
- **Migration Complexity**: Ensure that alternatives for removed parameters are documented and easy for clients to implement.  

Incrementing the version number when removing parameters ensures a transparent API evolution process, reducing integration risks and maintaining trust with consumers.

**Tags**: versioning, breaking changes, parameter removal, API contract, client communication.
<br><br>


### Always increment the version number of services when renaming operation parameters
Renaming operation parameters, whether in requests or responses, constitutes a breaking change. This
alteration can disrupt client applications relying on the original parameter names, leading to unexpected
failures or misinterpretations. Incrementing the version number ensures clients are aware of the change
and can update their implementations accordingly.  

Operation parameters are the inputs and outputs that define how a service communicates with clients. Renaming
these parameters, even with a minor adjustment, can break existing integrations by causing issues such as
invalid requests or missing data in responses.  

**Original request example**  
```json
{
  "userId": 123,
  "email": "example@example.com"
}
```  

**Modified request example (breaking change)**  
```json
{
  "user_id": 123,
  "email_address": "example@example.com"
}
```  

**Versioned endpoint examples**  
- `/v1/resource` (uses `userId` and `email`)  
- `/v2/resource` (uses `user_id` and `email_address`)  

**Recommendations**  
- **Versioning**: Increment the major version whenever parameter names are changed, regardless of how minor the adjustment may seem.  
- **Documentation**: Clearly detail parameter name changes in release notes, including a mapping between old and new names to assist clients in updating their requests and responses.  
- **Backward Compatibility**: Maintain support for the old parameter names in the previous version to provide a transition period for clients.  
- **Communication**: Notify clients in advance of planned parameter renaming, offering detailed guidance and example implementations for the new version.  

By versioning changes to parameter names, you safeguard client applications from unexpected disruptions and uphold the integrity of your service’s API.  
<br><br>


### Always increment the version number of services when there are changes in the behavior of an existing service operations
Changes to the behaviour of a service operation—such as modifying its logic, altering default values, or adjusting response
timing—constitute breaking changes. These updates can lead to unexpected outcomes for clients relying on the original behaviour,
necessitating an increment in the version number.  

Behaviour defines how a service processes requests and delivers responses. Alterations to this behaviour can affect client
workflows, assumptions, or processing logic, making it critical to communicate such changes through versioning.  

**Original behaviour example**  
- **Request**: `/v1/resource?status=active`  
- **Response**: Returns all active items, sorted by creation date.  

**Modified behaviour example (breaking change)**  
- **Request**: `/v2/resource?status=active`  
- **Response**: Returns only active items created in the last 30 days, sorted by relevance.  

**Versioned endpoint examples**  
- `/v1/resource` (original behaviour)  
- `/v2/resource` (updated behaviour)  

**Recommendations**  
- **Versioning**: Increment the major version for significant behavioural changes. For minor adjustments with minimal client impact, consider a minor version increment if backward compatibility is preserved.  
- **Documentation**: Clearly describe behavioural changes in release notes, including the rationale, affected operations, and expected client impact.  
- **Backward Compatibility**: Where possible, maintain support for the original behaviour through the older version to allow clients time for adaptation.  
- **Transition Support**: Provide guidance, examples, and test environments to assist clients in updating their integrations to the new behaviour.  

By versioning behavioural changes, you ensure transparency, minimise disruptions to client applications, and maintain
a predictable and reliable API evolution process.  
<br><br>


### Always increment the version number of services when there are changes in error codes of existing service operations
Modifying error codes for existing service operations constitutes a breaking change. Such changes disrupt the contract
between the service and its clients, potentially leading to misinterpretation of errors and unintended client behaviour. To
mitigate this, always increment the version number of the service when error codes are altered.

Error codes serve as a critical mechanism for communicating issues to clients. Updates such as introducing new error codes,
removing existing ones, or altering their meanings require careful handling to maintain clarity and stability in client integrations.  

**Original error code example**  
```json
{
  "errorCode": "INVALID_INPUT",
  "message": "The provided input is invalid."
}
```  

**Modified error code example (breaking change)**  
```json
{
  "error": {
    "code": "INPUT_ERROR",
    "description": "The provided input failed validation."
  }
}
```  

**Versioned endpoint examples**  
- `/v1/resource` (original error code structure)  
- `/v2/resource` (updated error code structure)  

**Recommendations**  
- **Versioning**: Increment the version number to reflect changes in error codes. Use major version increments for significant changes, such as modifying the structure or semantics, and minor increments for adding new error codes.  
- **Client Communication**: Clearly notify API consumers of the updated version, detailing changes and their implications in release notes or changelogs.  
- **Backward Compatibility**: Maintain older service versions to support existing error codes where feasible, ensuring a smooth transition for clients.  
- **Testing**: Provide a staging environment to help clients validate their integrations against the updated version before migrating.  

By versioning services appropriately, you uphold the reliability of client integrations and foster trust in the evolution of your API.
<br><br>


### Always increment the version number of services when there are changes in fault contracts of existing service operations
Changes to fault contracts, such as modifying error codes, altering error message structures, or adding/removing error types
for an existing service operation, constitute breaking changes. These updates require incrementing the service version to
ensure client applications remain functional without unexpected errors.

Fault contracts define the error-handling expectations for clients interacting with your service. Any changes to these
contracts can disrupt client-side error processing and lead to unexpected behaviour. Incrementing the version number
provides a clear indication of the update and allows clients to adapt at their own pace.

**Original fault contract**
```json
{
  "errorCode": "ERR001",
  "message": "Invalid request."
}
```

**Modified fault contract (breaking change)**
```json
{
  "error": {
    "code": "ERR001",
    "message": "Invalid request.",
    "details": "The 'id' field is required."
  }
}
```

**Versioned endpoint examples**
- `/v1/resource` (uses the original fault contract)
- `/v2/resource` (uses the updated fault contract)

**Recommendations**
- Carefully assess the impact of fault contract changes on existing clients.
- Document fault contract changes clearly in version release notes.
- Provide ample time for clients to transition to the updated version.
- Ensure the older service version continues to support existing fault contracts for backward compatibility, as feasible.
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


### Prefer using media type versioning for flexibility and clean URIs
When implementing API versioning, favour media type versioning by embedding the version information in
the `Content-Type` or `Accept` headers. This approach ensures cleaner URIs, better alignment with REST
principles, and improved flexibility in handling multiple versions of resources.

- **Header-Based Versioning**: Specify the API version within the media type (e.g., `application/vnd.example.v2+json`).  
- **Backward Compatibility**: Allow clients to request specific versions using the `Accept` header without altering the URI structure.  
- **Simplified URI Management**: Keep URIs consistent across versions to reduce complexity and maintain a more predictable API structure.  

**Examples**

**Client Request for a Specific Version**  
```http
GET /api/products/123
Accept: application/vnd.example.v2+json
```

**Response for Requested Version**  
```http
HTTP/1.1 200 OK
Content-Type: application/vnd.example.v2+json

{
  "id": 123,
  "name": "Laptop",
  "price": 999.99
}
```

**Scenarios**  
- **Incremental Changes**: Introducing new fields or formats without breaking older clients.  
- **Deprecation of Older Versions**: Gradually phasing out older versions while allowing clients to migrate at their own pace.  

**Cautions**  
- **Documentation Complexity**: Clearly document media types and their corresponding versions to avoid client confusion.  
- **Middleware Support**: Ensure that your server middleware or frameworks can correctly interpret versioned media types.  

**Tags**: versioning, media types, content negotiation, REST best practices.  
<br><br>