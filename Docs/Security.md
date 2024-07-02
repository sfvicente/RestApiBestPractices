# Security


## Data Transmission Security
These guidelines focus on securing data as it travels between the client and server.
<br>

### Always use HTTPS to encrypt data in transit, protecting sensitive information from being intercepted by malicious actors

// TODO: complement description

```http
// TODO: add example
```

See also: `HTTPS` `Encryption`
<br><br>


### Consider enforcing the use of HTTPS by implementing HSTS to protect against protocol downgrade attacks

// TODO: complement description

```http
// TODO: add example
```

See also: `HTTPS` `HSTS` `Encryption` `downgrade attack`
<br><br>


### Always protect data at rest by using encryption and secure storage mechanisms for sensitive information

// TODO: complement description

```http
// TODO: add example
```

See also: `data at rest` `Encryption` `storage` `confidentiality`
<br><br>


## Authentication and Authorization
Covers the mechanisms for verifying user identity and controlling access to resources
<br>


### Avoid submitting authentication credentials in the request body.

Although uncommon, it is a possible implementation for an API authentication. However this would indicate a non-RESTful design, which
is not recommended.

```http
// TODO: add example
```

// TODO: complement description

```http
// TODO: add example
```

See also: `authentication`
<br><br>


### Always implement authorization to control access to different resources and actions based on user roles and permissions

// TODO: complement description

```http
// TODO: add example
```

See also: `authorization` `access controls` `roles` `permissions`
<br><br>


## Input and Output Handling
Guidelines that address the validation and sanitation of data exchanged between clients and servers.
<br>

### Always validate all input data to prevent security vulnerabilities

// TODO: complement description
// such as SQL injection, cross-site scripting (XSS), and other attacks.

```http
// TODO: add example
```

See also: `SQL injection` `cross-site scripting` `XSS`
<br><br>



## Rate Limiting and Abuse Prevention
These guidelines focus on protecting the API from excessive usage and abuse.
<br>

## Secure Headers
These guidelines involve using HTTP headers to enhance security.
<br>


## Data Exposure and Endpoint Security
Ensures that the API exposes only necessary data and that endpoints are secured against unauthorized access
<br>


## Maintenance and Monitoring
Emphasizes the importance of ongoing security practices
<br>