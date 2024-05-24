# HTTP Headers
HTTP headers are the name or value pairs containing additional information that are transferred between clients and servers
with HTTP requests or responses.
<br>


## General
<br>


### Consider using standardized headers.

// TODO: add description

```http
// TODO: add example
```

// TODO: complement description

```http
// TODO: add example
```

<br><br>


## `Prefer` Header
The Prefer header is an HTTP request header used by clients to indicate their preferred server behaviors in processing
the request. It allows clients to suggest specific handling instructions without altering the fundamental request semantics.
<br>


### Consider supporting the `Prefer` header to handle processing preferences.

// TODO: add description.

<br><br>



## Custom Headers
Custom headers in HTTP are non-standard headers used to pass additional information between the client and the
server. These headers are typically defined by the developer and are used to meet specific application requirements
that are not covered by standard HTTP headers.
<br>


### Do not require custom headers for operating basic functionality of an API.

// TODO: add description

```http
// TODO: add example
```

// TODO: complement description

```http
// TODO: add example
```

<br><br>


### Consider using custom headers when services require additional functionality which is exposed via HTTP headers.

// TODO: add description

```http
// TODO: add example
```

// TODO: complement description

```http
// TODO: add example
```

<br><br>


### Prefix custom header names with `X-` for legacy systems or use clear, application-specific names.

// TODO: add description

```http
// TODO: add example
```

// TODO: complement description

```http
// TODO: add example
```

<br><br>