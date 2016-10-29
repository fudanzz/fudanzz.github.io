---
layout:     post
title:      "Rest API Design"
date:       2016-10-24 11:00:00
author:     "Phil"
header-img: "img/post-bg-01.jpg"
---

### API Overview


### API Design principle

- don’t surprise your end user
- focus on use cases
- copy successful APIs
- REST is not always best
- focus on developer experience


### API Design Process

- define your api biz value
- define your api metrics
- articulate your api use cases
- api schema model and best practice


### Rest API Design RuleBook

#### 1. URI Design

- Rule: Forward slash separator (/) must be used to indicate a hierarchical relationship
- Rule: Hyphens (-) should be used to improve the readability of URIs
- Rule: Underscores (_) should not be used in URIs
- Rule: Lowercase letters should be preferred in URI paths
- Rule: File extensions should not be included in URIs
- Rule: Consistent subdomain names should be used for your APIs
- Rule: Consistent subdomain names should be used for your client developer portal
- Rule: When modeling an API’s resources, we can start with the some basic resource archetypes:document,collection,store and controller
- Rule: A singular noun should be used for document names
- Rule: A plural noun should be used for collection names
- Rule: A plural noun should be used for store names
- Rule: A verb or verb phrase should be used for controller names
- Rule: CRUD function names should not be used in URIs
- Rule: The query component of a URI may be used to filter collections or stores
- Rule: The query component of a URI should be used to paginate collection or store results (may accept more complex inputs via a request’s entity body instead of the URI’s query part)

#### 2. HTTP Request/Response Design
- Rule: GET and POST must not be used to tunnel other request methods
- Rule: GET must be used to retrieve a representation of a resource
- Rule: HEAD should be used to retrieve response headers
- Rule: PUT must be used to both insert and update a stored resource
- Rule: PUT must be used to update mutable resources
- Rule: POST must be used to create a new resource in a collection
- Rule: POST must be used to execute controllers
- Rule: DELETE must be used to remove a resource from its parent
- Rule: OPTIONS should be used to retrieve metadata that describes a resource’s available interactions
- Rule: 200 (“OK”) should be used to indicate nonspecific success
- Rule: 200 (“OK”) must not be used to communicate errors in the response body
- Rule: 201 (“Created”) must be used to indicate successful resource creation
- Rule: 202 (“Accepted”) must be used to indicate successful start of an asynchronous action
- Rule: 204 (“No Content”) should be used when the response body is intentionally empty
- Rule: 400 (“Bad Request”) may be used to indicate nonspecific failure
- Rule: 401 (“Unauthorized”) must be used when there is a problem with the client’s credentials
- Rule: 403 (“Forbidden”) should be used to forbid access regardless of authorization state
- Rule: 404 (“Not Found”) must be used when a client’s URI cannot be mapped to a resource
- Rule: 405 (“Method Not Allowed”) must be used when the HTTP method is not supported
- Rule: 406 (“Not Acceptable”) must be used when the requested media type cannot be served
- Rule: 409 (“Conflict”) should be used to indicate a violation of resource state
- Rule: 412 (“Precondition Failed”) should be used to support conditional operations
- Rule: 415 (“Unsupported Media Type”) must be used when the media type of a request’s payload cannot be processed
- Rule: 500 (“Internal Server Error”) should be used to indicate API malfunction

#### 3. HTTP metadata Design
-



### Helpful website

1, http://test-cors.org/

2, http://enable-cors.org/

3, https://www.html5rocks.com/en/tutorials/cors/
