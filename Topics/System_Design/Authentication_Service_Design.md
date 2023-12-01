# Introduction: Designing an Authentication Service

**Authentication** is the first gateway users pass through when using any digital service to prove their identities. **Authorization** is how we ensure the *right people* are accessing the *right data*.
A well-designed authentication and authorization service has to strike the correct balance of security and user convenience. This balance shifts depending on what service you're offering; an in-browser casual multiplayer game will have completely different needs for security and user convenience compared to governmental corporate software.

## Table of Contents

1. [Types of Authentication](#auth-types)
	1. [Multi-Factor Authentication](#mfa)
	2. [Standardized Protocols](#protocols)
2. [Sessions and Tokens](#sessions-tokens)
	1. [Designing Token-Based Authentication](#token-design)
4. [Design Considerations](#auth-design)
5. [Common Technologies](#auth-common-tech)
6. [Further Reading](#further-reading)

## Types of Authentication <a name="auth-types"></a>

We all know about usernames and passwords, or **single-factor authentication**, which grants access to a system when the credentials are correct. However, in most modern systems, this is no longer the case for several reasons:
1. Users don't keep their passwords secure
2. Users are vulnerable to phishing schemes
3. Users easily forget their own credentials
4. Credentials can be easily cracked

A common theme we'll see is that authentication schemes will try to work around the weakest security link in the system, which are the users themselves. While small improvements can help, like security questions or increasing requirements for password hygiene (minimum N characters, with at least M special characters), modern approaches have better ways of working around this limitation. 

### Multi-Factor Authentication (MFA) <a name="mfa"></a>

Some MFA strategies require users to prove their credentials by demonstrating proof of *physical ownership* of an item. The most common among these is requiring the user to confirm their identity on a **separate device**, like a phone or a laptop; however, a really determined threat actor can bypass this by gaining remote access to the user's devices. 

The best option of MFA strategies is by making the user prove their *inherent characteristics*; that is, things that are unique to them that no one else can ever take from them. **Biometrics** are a good example of this; many smartphones will use fingerprints and facial recognition, as an example.

### Standardized Protocols <a name="protocols"></a>

Developers don't have to write everything from scratch; using a open protocol ensures that a service can have a standardized yet secure authentication mechanism. Several protocols exist (definitions from [this article](https://www.getkisi.com/blog/authentication-protocols-overview)):
1. **[LDAP (Lightweight Directory Access Protocol)](https://www.getkisi.com/glossary/lightweight-directory-access-protocol)** allows users to "securely locate organizations, individuals, and other resources such as files and devices in a network"
2. **[OAuth 2](https://tools.ietf.org/html/rfc6749)** is an "authorization framework that enables applications to obtain limited access to user accounts on an HTTP service, such as Facebook, GitHub, and DigitalOcean." 
3. **[SAML (Security Assertion Markup Language)](https://saml.xml.org/)** is an "XML-based, open-standard data format for exchanging authentication and authorization data between parties, in particular, between an identity provider and a service provider." SAML is often to provide Single Sign-On (SSO) to users, which allows to access different services using only one account.

## Sessions and Tokens <a name="sessions-tokens"></a>

Session and token-based authentication schemes allow users to avoid having to authenticate every single time they make a request over a service.

**Session-based authentication** is an older method that relies on the server to manage authentication. When a user logs in, the server generates a session, assigns a session ID stored in a browser cookie, and maintains authentication during the user's session on the site. While cookies are usually deleted upon logout, most modern browsers employ session restoring, retaining session cookies even after logout. This eliminates the need for repeated logins.

**Token-based authentication** creates an *encrypted token* upon user login, granting users the ability to perform activities on the site. Unlike session IDs stored on the server, the *client* retains the token, either in memory or in a cookie.
For session-based authentication, the server becomes complex with system or user scale. This is in contrast to token-based authentication; however, note that the latter may still involve storing API tokens in a database table for verification or revocation.

If you've ever heard of JSON Web Tokens (JWTs), that's a common form of token-based authentication! JWTs embed user data inside the token, allowing validation without database queries, making them suitable for serverless and stateless applications.

JWTs have several advantages:

1.  Compact size for quick transmission.
2.  Enhanced security through asymmetric encryption.
3.  Ubiquitous use due to the prevalence of JSON objects.
4.  Transparency in verifying senders and preventing tampering.

They also have drawbacks; for example, they make it harder to revoke access from the server side, leading to shorter expiration times to mitigate security risks; this can be annoying for a user.

### Designing Token-Based Authentication <a name="token-design"></a>
There's a few best practices to follow when we're building an authentication service using a token-based service:
1.  **Use Industry Standards:** Leverage established standards for token creation, such as OAuth 2.0 and OpenID Connect. Following widely accepted standards enhances interoperability and security.
2.  **Secure Token Storage:** Ensure secure storage of tokens on the client side. Avoid storing sensitive information in local storage or cookies susceptible to attacks. Use HTTP-only cookies for enhanced security.
3.  **Token Revocation:** Implement mechanisms for token revocation in case of security incidents or when a user logs out. Maintain a blacklist or use token introspection to check the validity of tokens.
4.  **Token Scoping:** Include a scope or permissions within the token to define the level of access granted to the client, and make sure to give the minimum possible amount of privileges.
5.  **Token Encryption:** When sensitive information is embedded in tokens, consider encrypting the token content. This adds an extra layer of security, especially for tokens containing user-specific data.
6.  **Implement Rate Limiting:** Protect against abuse by implementing rate limiting on token-related endpoints. This helps mitigate the risk of brute force attacks or other malicious activities.

## Design Considerations

When it comes to building an authentication service for any kind of digital service, particularly in the context of microservice architectures, the best approach is to "use an API gateway—this is a service deployed in front of the microservices application, which serves as a single endpoint for all user requests." A good example of this are [interceptors in Axios](https://axios-http.com/docs/interceptors). Every API call in an mobile app or web service will pass through this checkpoint; it'll do something like attach a token, ensure a token is valid, or catch unauthorized access attempts. Other services sending requests to this checkpoint won't be aware of the underlying service at this gateway; it'll just package the requests accordingly, authenticate, and forward them. 

## Common Technologies <a name="auth-common-tech"></a>
1.  **OpenID Connect:** Built on top of OAuth 2.0, OpenID Connect provides an identity layer that enables clients to verify the identity of end-users based on the authentication performed by an authorization server. It's often used for single sign-on (SSO) scenarios.
2. **Auth0** is a cloud-based identity and access management (IAM) platform that provides authentication and authorization services for web, mobile, and legacy applications. It allows developers to add secure and seamless authentication to their applications without having to manage the complexity of identity infrastructure. Auth0 is often used to implement features such as single sign-on (SSO), social login, multi-factor authentication (MFA), and more.
3. **Kerberos** is a "network authentication protocol. It is designed to provide strong authentication for client/server applications by using secret-key cryptography. A free implementation of this protocol is available from the Massachusetts Institute of Technology. Kerberos is available in many commercial products as well." ([Source](https://www.getkisi.com/blog/authentication-protocols-overview))

## Further Reading <a name="further-reading"></a>
[TryExponent: Authentication & Authorization](https://www.tryexponent.com/courses/fundamentals-system-design/authentication-authorization)
[FrontEgg: How Does Authentication Work?](https://frontegg.com/blog/authentication#How-Does-Authentication-Work)
[Tzachi Strugo: Authentication & Authorization in Microservices Architecture](https://dev.to/behalf/authentication-authorization-in-microservices-architecture-part-i-2cn0)
