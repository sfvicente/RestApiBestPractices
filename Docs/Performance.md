# Performance

<br>


## General
<br>


### Applications should be designed and implemented to reduce bandwidth requirements and improve responsiveness.

// TODO: add description.

```http
// TODO: add example
```

<br><br>


### Applications should support pagination to limit access to large collections of data items, thus reducing network traffic.

// TODO: add description.

```http
// TODO: add example
```

<br><br>



## Compression
<br>


### Considering compressing the payload of response messages before sent back to the client.

As a general guideline, compress the payload of response messages with gzip, unless there are requirements not to do it.

// TODO: complement description.

```http
// TODO: add example
```

<br><br>


### Do not use compression if the amount of requests being served is so high that compression time becomes a bottleneck.

// TODO: add description.

```http
// TODO: add example
```

<br><br>


### Even when using compression by default, servers should also support payload without compression.

// TODO: add description.

```http
// TODO: add example
```

<br><br>


### A server should indicate it is using gzip compression via the `Content-Encoding` header.

// TODO: add description.

```http
// TODO: add example
```

<br><br>

