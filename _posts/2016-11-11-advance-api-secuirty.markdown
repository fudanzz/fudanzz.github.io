---
layout:     post
title:      "Advanced API Security"
date:       2016-10-28 11:00:00
author:     "Phil"
header-img: "img/post-bg-01.jpg"
---

### API Overview
APU economy is booming.

Security, rate limiting (throttling), and monitoring are key aspects of a managed business API. It also must have the ability to scale up and down for high availability based on traffic.

Life-cycle management is another key differentiator between a naked API and a managed API

A comprehensive API management platform needs to have at least three main components: a publisher, a store, and a gateway

### Design Principles
The CIA triad (confidentiality, integrity, and availability) is one of the core principles of information security. In achieving CIA, authentication, authorization, nonrepudiation, and auditing play a vital role

### security pattern
Direct Authentication Pattern (own user store)
Brokered Authentication Pattern (no inbound in green zone)
Policy-Based Access Control Pattern

### Thread modelling
STRIDE stands for Spoofing, Tampering, Repudiation, Information disclosure, Denial of service, Escalation of privileges

### API Security Detail
- HTTP Basic Authentication and Digest Authentication are the most-used authentication schemes for many APIs prior to the OAuth era

- Transport Layer Security (TLS) mutual authentication, also known as client authentication or two-way Secure Socket Layer (SSL), is part of the TLS handshake process. In one-way TLS, only the server proves its identity to the client; this is mostly used in e-commerce to win consumer confidence by guaranteeing the legitimacy of the e-commerce vendor. In contrast, mutual authentication authenticates both parties—the client and the server.

- The identity delegation model discussed here is the foundation for almost all delegated access-control models used at present
