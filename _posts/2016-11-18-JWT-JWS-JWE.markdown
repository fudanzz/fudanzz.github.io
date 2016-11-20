---
layout:     post
title:      "JWT vs JWS vs JWE"
date:       2016-11-18 11:00:00
author:     "Phil"
header-img: "img/post-bg-01.jpg"
---

### JWT Overview

JSON Web Token (JWT) defines a container to transport data between interested parties in JSON. The ongoing work of the JWT specification group under IETF is available at

 (https://datatracker.ietf.org/doc/draft-ietf-oauth-json-web-token/)

In other words, a JWT claims (i.e., claims represented in JSON format) could be sent either as JWS structure or JWE structure (or both; more on that later) depending on what you are trying to achieve. So, when you are sending JWT to someone, it is essentially either a JWS payload or a JWE payload.

### JWS

As the name suggests, JWS scheme digitally signs the content. The content to be carried here are JWT claims. The server signs the JWT and sends it to the client, say after successful user authentication. The server expects the client to send this JWS back to the server as part of the next request.

What if the client we're dealing with is rogue? That's where the signature comes in. Signature brings Integrity (remember the Confidentiality, Integrity, Availability triad?) and Authentication  into the equation. In other words, server can be sure that the JWT claims inside the JWS it just received were not tampered with either by the rogue client or by a man-in-the-middle.

Server achieves this by validating the signature of the message to ensure that the claims were not tampered with by the client. If the server detects any kind of tampering, it can take appropriate action (deny the request or block the client etc.).

The client can also validate the signature. To do so, the client either needs server's secret (if the JWT signature is HMAC) or needs server's public key (if the JWT was digitally signed).

Note: With JWS, the payload (claims portion) is not encrypted. So, don't send anything sensitive.

### JWE
The JWE scheme encrypts the content instead of signing it. The content being encrypted here are JWT claims. JWE, thus brings Confidentiality. The JWE can be signed and enclosed in a JWS. Now, you get both encryption and signature (thus getting Confidentiality, Integrity, Authentication).

The JOSE Header for a JWS can also be distinguished from the JOSE Header for a JWE by determining whether an "enc" (encryption algorithm) member exists. If the "enc" member exists, it is a JWE; otherwise, it is a JWS.


Note: credit to https://securedb.co/community/jwt-vs-jws-vs-jwe/
