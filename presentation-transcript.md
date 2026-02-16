# SLIDE 1 – Title

Today I will talk about modern authentication mechanisms, focusing on OAuth 2.0 and JSON Web Tokens.  

These technologies are fundamental in modern web development.  

They are used in mobile applications, cloud-native systems, microservices, and third-party integrations.  

In this talk, I will explain the conceptual difference between authentication and authorization, describe how OAuth works, how JWT is structured, and why they are often used together.

---

# SLIDE 2 – Authentication vs Authorization

First, it is important to clearly distinguish authentication and authorization.  

Authentication answers the question: who are you?  

It verifies identity using credentials, such as a password, biometrics, or multi-factor authentication.  

Authorization answers a different question: what are you allowed to do?  

It defines permissions, roles, and access scopes.  

Although these two concepts are often implemented together, they solve different problems.  

OAuth mainly addresses authorization, while JWT is commonly used to carry identity and permission data.

---

# SLIDE 3 – Traditional Session-Based Authentication

Traditionally, web applications relied on session-based authentication.  

After login, the server creates a session and stores it in memory or in a database.  

The client receives a session ID stored in a cookie.  

On each request, the server validates this session ID.  

This model works well in monolithic systems.  

However, in microservices and distributed systems, it becomes problematic because session state must be shared between instances.  

That introduces synchronization complexity and scaling limitations.

---

# SLIDE 4 – OAuth 2.0 Overview

OAuth 2.0 is an authorization framework designed for delegated access.  

It allows a user to grant limited access to their resources without sharing credentials.  

For example, when you log in to a service using Google or GitHub, OAuth is working behind the scenes.  

Instead of giving your password to the client application, you grant permission, and the system issues an access token.  

That token represents the delegated authority.

---

# SLIDE 4.1 – OAuth Roles

OAuth defines four main roles.  

The Resource Owner is usually the user who owns the data.  

The Client is the application requesting access.  

The Authorization Server authenticates the user and issues tokens.  

The Resource Server hosts protected resources and validates the access token.  

These roles may be implemented within the same system or separated across services.

---

# SLIDE 4.2 – Authorization Code Flow

The Authorization Code Flow is the most widely used OAuth flow.  

First, the client redirects the user to the authorization server.  

The user authenticates and grants consent.  

The authorization server returns an authorization code to the client.  

The client then exchanges that code for an access token using a secure back-channel request.  

This design prevents exposing access tokens directly in the browser and improves security.

---

# SLIDE 5 – JWT Overview

JWT stands for JSON Web Token.  

It is a compact, URL-safe format for transmitting information as a JSON object.  

JWTs are digitally signed, which ensures data integrity and authenticity.  

They are commonly used as access tokens in OAuth-based systems.  

Since the token contains all necessary claims, the server does not need to store session data.

---

# SLIDE 5.1 – JWT Structure

A JWT consists of three parts: header, payload, and signature.  

The header defines the signing algorithm.  

The payload contains claims such as user ID, roles, issued-at time, and expiration.  

The signature is generated using a secret or private key and ensures the token has not been modified.  

If any part of the payload changes, the signature becomes invalid.

---

# SLIDE 5.2 – JWT Pros and Cons

JWT provides stateless authentication, which improves scalability in distributed systems.  

It works well across domains and microservices.  

However, there are risks.  

If a token is leaked, it can be used until it expires.  

JWT does not support immediate revocation by default.  

Therefore, best practices include short-lived tokens, refresh tokens, HTTPS-only transmission, and secure key management.

---

# SLIDE 6 – OAuth + JWT Together

OAuth and JWT are complementary technologies.  

OAuth defines the authorization framework and the flow for obtaining access.  

JWT defines the format of the token itself.  

In modern architectures, the Authorization Server often issues a JWT as the access token.  

The Resource Server can validate the JWT locally without making additional network calls.  

This combination enables scalable and secure API-based systems.

---

# SLIDE 7 – Comparison

Comparing session-based authentication and OAuth with JWT, we see key differences.  

Sessions are stateful and require shared storage but allow immediate revocation.  

OAuth with JWT is stateless and highly scalable, especially for APIs and microservices.  

However, token revocation is more complex and typically relies on expiration time.

---

# SLIDE 8 – Summary

To summarize, OAuth 2.0 is an authorization framework that enables delegated access.  

JWT is a compact, signed token format used to transmit identity and permission data.  

Together, they form the foundation of modern authentication and authorization systems in cloud-native architectures.
