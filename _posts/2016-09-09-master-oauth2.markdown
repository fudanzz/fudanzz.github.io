---
layout:     post
title:      "OAuth2.0 reading notes"
subtitle:   ""
date:       2016-09-09 23:00:00
author:     "Phil"
header-img: "img/post-bg-06.jpg"
---

## Overview
<p>OAuth 2.0 is a protocol that allows distinct parties to share information and resources in a secure and reliable manner.</p>   

<p>Strictly speaking, the OAuth 2.0 protocol is actually an authorization protocol and not an authentication protocol.</p>

<p>OAuth 2.0 involve two things:</p>

* Allowing a user to log into an application with another account. For example, Pinterest allowing users to log in with their Twitter accounts. This is known as **federated identity**.

* Allowing one service to access resources on another service on behalf of the user. For example, Adobe accessing your Facebook photos on your behalf. This is known as **delegated authority**.

<p>Four main grant typea:</p>

* Authorization code grant
* Implicit grant
* resource owner password credentials (not recommend)
* The client credentials(not recommend)

## Implicit grant(client side flow)

Implicit grant type suited for untrusted case:  access token is provided.

### Pros

There is a convenient pro for being an untrusted client:

**Simplicity**: Due to the straightforward design, this solution is very simple to implement. Since all of the work happens in the browser, no backend servers or data stores are required for such an application. (If they had these, they could be considered trusted.)

### Cons

However, here are the cons:

* Less security: The key must be relayed to the browser for the client application to use. The browser is considered public and so this key may easily fall into the hands of another user.

* Short-term access only: Since the client is untrusted, they cannot store keys for long-term use. Because of this, the user will have to reauthenticate and regrant access more often than with a trusted client.

## Authorization code grant(server side flow)



resource owner password : (end user credential is provided)

user provide credential to client app, client app request the access token on behalf of end user

client credential: (no end user is involved)
client app request the token directly
