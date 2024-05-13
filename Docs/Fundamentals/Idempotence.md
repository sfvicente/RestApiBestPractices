# Idempotence

## Introduction

Idempotence is a fundamental concept in the context of RESTful APIs, defining the behavior of HTTP methods when applied
to resources. An idempotent operation is one that can be applied multiple times without changing the result beyond
the initial application. In other words, performing an idempotent operation once or multiple times should leave
the resource state unchanged after the first application.

## Idempotent and Safe Methods

Within REST, an idempotent method guarantees that repeated identical requests will have the same effect as a single
request. This property is ensures predictable behavior and resilience in distributed systems.

Safe methods are HTTP methods that do not modify the state of a resource on the server. They are read-only operations
that retrieve data without causing any side effects. For example, the `GET` and `HEAD` methods are considered safe
because they retrieve information about a resource without altering it.

While safe methods focus on not modifying resource state, idempotent methods ensure that repeated identical requests 
produce the same result as a single request. Not all safe methods are idempotent, and vice versa. For instance, the
`GET` method is both safe (read-only) and idempotent (retrieving the same resource repeatedly yields the same result). On
the other hand, the `POST` method is not safe (it creates a new resource) and not idempotent (multiple identical POST
requests can result in the creation of multiple resources).

Below is an identification of idempotence and safety characteristics of common HTTP methods:

| Method  | Idempotent? | Safe? |
|---------|-------------|-------|
| GET     | Yes         | Yes   |
| POST    | No          | No    |
| PUT     | Yes         | No    |
| DELETE  | Yes         | No    |
| PATCH   | No          | No    |
| HEAD    | Yes         | Yes   |
| OPTIONS | Yes         | Yes   |
| TRACE   | Yes         | Yes   |


Understanding the idempotent and safe nature of HTTP methods allows for designing robust and predictable RESTful 
APIs. Idempotent methods ensure that operations can be retried safely without unintended side effects, contributing
to the reliability and scalability of API interactions.



