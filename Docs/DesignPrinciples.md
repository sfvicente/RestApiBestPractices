# Design Principles


## General



### Never maintain transient state information between requests.

REST APIs use a stateless request model.

// TODO: complement description

HTTP requests can occur in any order.

<br><br>


### Design operations to be atomic.

By designing the API under this principle, each request becomes an atomic operation.

// TODO: complement description

```http
// TODO: add examples
```
<br><br>



## ...