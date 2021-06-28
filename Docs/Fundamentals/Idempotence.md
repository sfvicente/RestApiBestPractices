# Idempotence

## Introduction

...


 Withing the context of REST, idempotency is property of an HTTP method that results in the same state change of a resource, whether 
 applying the method multiple times or a single time to a resource. Even though the response maybe different, the state would
 remain identical.
 
 For example, the `GET` method would be considered safe as applying it to a resource would not result in a change of state for that
 resource. The `GET`, `PUT` and `DELETE` methods are idempotent.


 ...


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

## ...



