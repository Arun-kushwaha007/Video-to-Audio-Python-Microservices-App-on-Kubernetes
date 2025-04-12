# JWT: JSON Web Token

## What are JWT?

JWT are open industry standard method for representing claims securely between two parties. It is a compact, URL-safe means of representing claims to be transferred between two parties. The token is digitally signed and contains a payload that can be verified and trusted.

### Example:

eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJzdWIiOiIxMjM0NTY3ODkwIiwibmFtZSI6IkpvaG4gRG9lIiwiYWRtaW4iOnRydWUsImlhdCI6MTUxNjIzOTAyMn0.KMUFsIDTnFmyG3nMiGM6H9FNFUROf3wh7SmqJp-QV30


The above JWT token is divided into 3 parts with a dot (`.`) in between them. They are:

1. **Header**: Algorithm (for encryption) and Token type  
2. **Payload**: Data  
3. **Signature**: Digital signature  

All of the above are encrypted and can be decoded using a JWT decoder tool.

---

## Q: What is the difference between JWT and OAuth?

**A**: JWT and OAuth are two different concepts in the field of authentication and authorization.  
- JWT is a token-based authentication mechanism.  
- OAuth is an authorization framework that allows users to grant third-party applications limited access to their resources on another service provider's website.  

In other words, JWT is used for **authentication**, while OAuth is used for **authorization**.

---

## Q: How do you securely store a JWT on the client-side?

**A**: You should never store a JWT on the client-side in plain text.  
Instead, you should store it securely using a secure storage mechanism such as:

- LocalStorage  
- Cookies with the `Secure` and `HttpOnly` flags set  

This will prevent the JWT from being accessed by malicious scripts.  
Additionally, you should use a secure protocol such as **HTTPS** to transmit the JWT between the client and server.

---

## Q: What are the common use cases of JWT?

JWT is commonly used in the following scenarios:

1. Authentication: JWT is used to authenticate users and verify their identity.  
2. Authorization: JWT is used to authorize users to access specific resources or perform certain actions.  
3. Single Sign-On (SSO): JWT is used to implement SSO, allowing users to access multiple applications with a single set of credentials.  
4. Microservices Architecture: JWT is used to authenticate and authorize requests between microservices.  
5. API Security: JWT is used to secure APIs by authenticating and authorizing requests.  
6. Identity Management: JWT is used to manage user identities and authenticate users across multiple applications.  
7. Access Control: JWT is used to control access to resources and ensure that only authorized users can access them.  
8. Session Management: JWT is used to manage user sessions and authenticate users without storing session data on the server.  
9. Real-time Web Applications: JWT is used to authenticate and authorize users in real-time web applications.  
10. Mobile and Web Applications: JWT is used to authenticate and authorize users in mobile and web applications.

---

## Q: How can you invalidate a JWT token?

There are several ways to invalidate a JWT token:

1. **Token Blacklisting**: You can store the JWT token in a blacklist database and check if the token is present in the blacklist before verifying it.  
2. **Token Revocation**: You can implement a token revocation mechanism that allows users to revoke their tokens.  
3. **Token Expiration**: You can set an expiration time for the JWT token, after which it becomes invalid.  
4. **Token Refresh**: You can implement a token refresh mechanism that allows users to obtain a new token after the previous one has expired.  
5. **Token Signature Change**: You can change the signature of the JWT token, making the previous token invalid.

---

## JWT vs Sessions

JWT vs sessions are two different approaches to handle user authentication and authorization. Here are some key differences between them:

1. **Storage**: JWT is stored on the client-side, while sessions are stored on the server-side.  
2. **Security**: JWT is more secure than sessions because it uses a digital signature to prevent tampering and ensures that the token is not modified during transmission.  
3. **Scalability**: JWT is more scalable than sessions because it does not require a database to store session data.  
4. **Complexity**: JWT is more complex than sessions because it requires a good understanding of token-based authentication and authorization.  
5. **Performance**: JWT is faster than sessions because it does not require a database query to retrieve session data.  
6. **Statelessness**: JWT is stateless, meaning that the server does not store any information about the user's session. Sessions, on the other hand, are stateful, meaning that the server stores information about the user's session.  
7. **Token-based**: JWT is token-based, meaning that the user is authenticated using a token.  
8. **Session-based**: Sessions are session-based, meaning that the user is authenticated using a session ID.  
9. **Authentication**: JWT is used for authentication, while sessions are used for both authentication and authorization.
