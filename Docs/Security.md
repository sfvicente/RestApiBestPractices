# Security


## Data Transmission Security
These guidelines focus on securing data as it travels between the client and server.
<br>

### Always use HTTPS to encrypt data in transit and protect against interception

// TODO: complement description

```http
// TODO: add example
```

See also: `HTTPS` `Encryption`
<br><br>


### Consider enforcing the use of HTTPS by implementing HSTS to protect against protocol downgrade attacks
To strengthen security and ensure encrypted communication between clients and servers, consider enforcing HTTPS by implementing
HTTP Strict Transport Security (HSTS). HSTS is a web security policy mechanism that forces web browsers to interact with your
server over HTTPS only, effectively preventing protocol downgrade attacks and protecting against man-in-the-middle attacks. By
enforcing HTTPS, you provide a secure environment for transmitting sensitive data and ensure clients always connect over a
secure protocol.

When a client accesses the server for the first time over HTTPS, the server can include an HSTS header in the response,
instructing the client to only use HTTPS for all future requests.

**Key Points:**
- **Prevents protocol downgrade**: Eliminates the risk of clients unintentionally using an insecure HTTP connection.
- **Protects against man-in-the-middle attacks**: Keeps all client-server communication encrypted.
- **Enforces secure connection**: Ensures all users access resources over HTTPS, improving overall API security.

**Example of setting an HSTS header in a response:**
```http
HTTP/1.1 200 OK
Content-Type: application/json
Strict-Transport-Security: max-age=31536000; includeSubDomains
```

In this example, the `Strict-Transport-Security` header tells the client to only connect over HTTPS for the next 31536000
seconds (1 year). The `includeSubDomains` directive applies this policy to all subdomains, ensuring secure access across the entire domain.

See also: `HTTPS` `HSTS` `Encryption` `downgrade attack`
<br><br>


### Always protect data at rest by using encryption and secure storage mechanisms for sensitive information
To safeguard sensitive data stored on servers, databases, or backups, always employ encryption and secure storage mechanisms
for data at rest. Encrypting sensitive information ensures that even if unauthorized access occurs, the data remains unreadable
without the encryption key. Additionally, storing data in secure, restricted environments further reduces the risk of exposure
or tampering.

Sensitive information, such as personally identifiable information (PII), financial data, or authentication tokens, should be
encrypted using strong, industry-standard algorithms (e.g., AES-256). Implementing access control policies around the storage
environment further enhances security by ensuring that only authorized personnel can access this data.

**Key Points:**
- **Ensures data privacy**: Protects sensitive information from unauthorized access.
- **Reduces risk of exposure**: Encryption renders data unreadable without the necessary decryption keys.
- **Strengthens compliance**: Meets regulatory requirements for data security and privacy, such as GDPR or HIPAA.

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


### Always ensure that tokens have a limited lifespan

// TODO: complement description

```http
// TODO: add example
```

See also: `tokens` `expiration`
<br><br>


### Always provide mechanisms for revoking tokens if they are compromised

// TODO: complement description

```http
// TODO: add example
```

See also: `tokens` `revocation`
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


### Always sanitize output data to ensure that it does not contain any sensitive information or malicious content

// TODO: complement description

```http
// TODO: add example
```

Tags: `data exposure`
<br><br>


### Never expose detailed error messages or stack traces to the client

// TODO: complement description

```http
// TODO: add example
```

Tags: `error handling` `error messages` `stack trace` `data exposure`
<br><br>


### Always log detailed errors server-side

// TODO: complement description

```http
// TODO: add example
```

Tags: `error handling` `error messages`
<br><br>


## Rate Limiting and Abuse Prevention
These guidelines focus on protecting the API from excessive usage and abuse.
<br>


### Consider implementing rate limiting to prevent abuse and protect from denial-of-service (DoS) attacks

// TODO: complement description

```http
// TODO: add example
```

Tags: `rate limiting` `denial-of-service` `DoS`
<br><br>


### Always monitor and log activity to detect and respond to suspicious behavior

// TODO: complement description

```http
// TODO: add example
```

Tags: `monitoring` `logging`
<br><br>


### Always keep logs secure

// TODO: complement description

```http
// TODO: add example
```

Tags: `logging` `data exposure`
<br><br>


### Consider reviewing logs regularly

// TODO: complement description

```http
// TODO: add example
```

Tags: `logging`
<br><br>


## Secure Headers
These guidelines involve using HTTP headers to enhance security.
<br>


## Data Exposure and Endpoint Security
Ensures that the API exposes only necessary data and that endpoints are secured against unauthorized access
<br>


### Always return only the data necessary for the client to function

// TODO: complement description

```http
// TODO: add example
```

Tags: `data exposure`
<br><br>


### Always avoid exposing sensitive information

// TODO: complement description

```http
// TODO: add example
```

Tags: `data exposure`
<br><br>


### Always ensure that all endpoints are secure and follow the principle of least privilege

// TODO: complement description

```http
// TODO: add example
```

Tags: `endpoint security` `least privilege`
<br><br>


### Do not expose unnecessary endpoints

// TODO: complement description

```http
// TODO: add example
```

Tags: `data exposure` `endpoint security`
<br><br>


## Maintenance and Monitoring
Emphasizes the importance of ongoing security practices
<br>


### Consider conducting regular security audits and penetration testing to identify and fix vulnerabilities

// TODO: complement description

```http
// TODO: add example
```

Tags: `security audit` `penetration testing` `vulnerabilities`
<br><br>


### Consider regularly updating dependencies and libraries to protect against known vulnerabilities

// TODO: complement description

```http
// TODO: add example
```

Tags: `dependency management` `vulnerabilities`
<br><br>