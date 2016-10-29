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
- Rule: The query component of a URI should be used to paginate collection or store results

### Helpful website

1, http://test-cors.org/

2, http://enable-cors.org/

3, https://www.html5rocks.com/en/tutorials/cors/
