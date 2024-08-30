# 02. OAuth and JWT

## Overview

OAuth (Open Authorization) and JWT (JSON Web Token) are two essential technologies used in modern web applications to handle authentication and authorization securely. OAuth is a protocol that allows third-party applications to access user data without sharing passwords, while JWT is a compact, URL-safe means of representing claims to be transferred between two parties. This lesson will explore the principles of OAuth and JWT, how they work together, their advantages, disadvantages, and common use cases.

## What is OAuth?

**Definition**: OAuth is an open standard for access delegation commonly used as a way to grant websites or applications limited access to user information without exposing passwords. It enables users to authorize third-party applications to access their data on another service without sharing their credentials.

### Key Components of OAuth

1. **Resource Owner**: The user who owns the data and grants access to a third-party application.

2. **Client**: The application that wants to access the user's data. It must be registered with the authorization server.

3. **Authorization Server**: The server that authenticates the user and issues access tokens to the client after obtaining user consent.

4. **Resource Server**: The server that hosts the user's data and accepts access tokens to grant access to the requested resources.

5. **Access Token**: A token issued by the authorization server that the client uses to access the resource server on behalf of the user.

### OAuth Flow

1. **Authorization Request**: The client redirects the user to the authorization server, requesting access to specific resources.

2. **User Consent**: The user authenticates and grants permission for the client to access their data.

3. **Authorization Grant**: The authorization server issues an authorization grant (e.g., authorization code) to the client.

4. **Access Token Request**: The client exchanges the authorization grant for an access token by making a request to the authorization server.

5. **Access Token Response**: The authorization server responds with an access token (and optionally a refresh token).

6. **Resource Access**: The client uses the access token to make requests to the resource server, accessing the user's data.

### Advantages of OAuth

1. **Delegated Access**: OAuth allows users to grant limited access to third-party applications without sharing their passwords.

2. **Granular Permissions**: Users can control what data and actions third-party applications can access.

3. **Improved Security**: OAuth reduces the risk of credential theft by not requiring users to share their passwords with third-party applications.

### Disadvantages of OAuth

1. **Complexity**: Implementing OAuth can be complex, requiring careful management of tokens and user consent flows.

2. **Token Management**: Managing access and refresh tokens can introduce additional overhead and potential security risks if not handled correctly.

3. **User Experience**: The authorization flow may require additional steps for users, potentially impacting user experience.

## What is JWT?

**Definition**: JSON Web Token (JWT) is an open standard (RFC 7519) that defines a compact and self-contained way to securely transmit information between parties as a JSON object. JWTs are used primarily for authentication and information exchange.

### Key Components of JWT

1. **Header**: Contains metadata about the token, including the type of token (JWT) and the signing algorithm used (e.g., HMAC, RSA).

2. **Payload**: Contains the claims, which are statements about an entity (typically, the user) and additional data. Claims can be standard (e.g., `sub`, `iat`, `exp`) or custom.

3. **Signature**: The signature is created by combining the encoded header and payload, then signing it using a secret key or a public/private key pair. This ensures that the token has not been tampered with.

### JWT Structure

A JWT is represented as three Base64Url-encoded strings separated by dots (`.`):

```
eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJzdWIiOiIxMjM0NTY3ODkwIiwibmFtZSI6IkpvaG4gRG9lIiwiaWF0IjoxNTE2MjM5MDIyfQ.SflKxwRJSMeKKF2QT4fwpMeJf36POk6yJV_adQssw5c
```

- **Header**: `eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9`
- **Payload**: `eyJzdWIiOiIxMjM0NTY3ODkwIiwibmFtZSI6IkpvaG4gRG9lIiwiaWF0IjoxNTE2MjM5MDIyfQ`
- **Signature**: `SflKxwRJSMeKKF2QT4fwpMeJf36POk6yJV_adQssw5c`

### Advantages of JWT

1. **Compact**: JWTs are compact and can be easily transmitted in HTTP headers or URL parameters.

2. **Self-Contained**: JWTs carry all the necessary information about the user, reducing the need for database lookups.

3. **Interoperability**: Since JWTs are based on JSON, they can be easily used across different programming languages and platforms.

4. **Security**: The signature ensures the integrity and authenticity of the token, preventing tampering.

### Disadvantages of JWT

1. **Token Size**: JWTs can become large if they contain many claims, potentially impacting performance when transmitted over the network.

2. **Revocation**: Once issued, JWTs cannot be easily revoked. If a token is compromised, it remains valid until it expires.

3. **Complexity**: Implementing JWTs securely requires careful consideration of signature algorithms and key management.

## OAuth and JWT Together

OAuth and JWT are often used together in modern applications for secure authentication and authorization:

- **OAuth as the Authorization Framework**: OAuth provides the framework for granting access to resources without sharing passwords. It defines how access tokens are issued and used.

- **JWT as the Access Token**: JWTs are commonly used as access tokens in OAuth implementations. They allow clients to access protected resources while carrying claims about the user and their permissions.

### Example Flow

1. **User Authentication**: The user authenticates with the authorization server using OAuth.

2. **Access Token Issuance**: Upon successful authentication, the authorization server issues a JWT as the access token.

3. **Resource Access**: The client uses the JWT to access protected resources on the resource server, including the JWT in the Authorization header of HTTP requests.

4. **Token Validation**: The resource server validates the JWT by verifying its signature and checking claims (e.g., expiration, audience) before granting access.

## Conclusion

OAuth and JWT are essential technologies for securing modern applications by facilitating secure authentication and authorization. Understanding how they work together allows developers to build robust security mechanisms that protect sensitive user data while enabling seamless access to resources. By implementing OAuth with JWTs, organizations can enhance their security posture and provide a better user experience.

Next: [03. Encryption and Hashing](./03-encryption-and-hashing.md)
