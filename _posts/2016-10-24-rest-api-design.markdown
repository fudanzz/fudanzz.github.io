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


### preflight request

there are preflight request under DELETE,PUT request

—> a preflight request must have an HTTP OPTIONS method, and it must contain an Origin and Access-Control-Request-Method header

—>for server side response:


    var handleCors = function(req, res, next) {
       res.set('Access-Control-Allow-Origin', 'http://localhost:1111');
     if (isPreflight(req)) {
    res.set('Access-Control-Allow-Methods', 'GET, DELETE');
      res.status(204).end();
     return;
    }

other could trigger preflight options request:  CORS request with customised http headers

- The browser sends a preflight request to ask the server for permission to make the actual request.
- The preflight request protects servers from receiving unexpected requests.
- The preflight request asks permissions to make requests with certain HTTP
- methods and/or add custom HTTP headers to the request.
- The preflight request takes the form of an HTTP OPTIONS method with an Ori-
- gin and Access-Control-Request-Method header.
- The server can grant permissions to use certain HTTP methods by using the
- Access-Control-Allow-Methods header. The server can also grant permission to use certain HTTP headers by using the Access-Control-Allow-Headers header.
- The preflight result cache is a performance optimization that helps reduce the number of preflight requests made to a particular endpoint.

■ The Access-Control-Allow-Credentials header can be used in conjunction with XMLHttpRequest’s withCredentials property to include cookies on cross-origin requests.

■ The Access-Control-Expose-Headers header can be used to expose response headers to the client.

### Best Practice

- Access-Control-Allow-Origin:

    – &nbsp;&nbsp;Use the * value to allow requests from all origins.

    – &nbsp;&nbsp;Use a whitelist to allow only certain origins.

- Access-Control-Allow-Credentials:

    – &nbsp;&nbsp;Setting the value to true allows cookies on requests.

    – &nbsp;&nbsp;Enable cookies only if you’re sure you need them.

    – &nbsp;&nbsp;If your server does support cookies, be sure to also validate the origin and
implement CSRF protection.

Access-Control-Allow-Methods:

– &nbsp;&nbsp;This header only needs to be present on preflight responses.

– &nbsp;&nbsp;It indicates which HTTP methods are allowed on a URL.

– &nbsp;&nbsp;Common values include HEAD, OPTIONS, GET, POST, PUT, PATCH, and DELETE.

- Access-Control-Allow-Headers:

– &nbsp;&nbsp;This header only needs to be present on preflight responses.

– &nbsp;&nbsp;It indicates which HTTP headers are allowed on a URL.

– &nbsp;&nbsp;Echo the Access-Control-Request-Headers value to get full header support.

- Access-Control-Max-Age:

– &nbsp;&nbsp;This header only needs to be present on preflight responses.

– &nbsp;&nbsp;It indicates how many seconds to cache preflight requests for.

– &nbsp;&nbsp;Browsers may have their own maxAge caps.

- Access-Control-Expose-Headers:

– &nbsp;&nbsp;This header indicates which response headers to expose to clients.

– &nbsp;&nbsp;It’s an optional header that isn’t required for a successful CORS request.

### Simple node server example

    var express = require('express');
    var app = express();

    app.use(function (req, res, next) {
        res.header('Access-Control-Allow-Origin', '*');
         res.header('Access-Control-Allow-Headers', 'Origin,X-Requested-With, Content-Type,Accept');
        next();
    });


### Helpful website

1, http://test-cors.org/

2, http://enable-cors.org/

3, https://www.html5rocks.com/en/tutorials/cors/