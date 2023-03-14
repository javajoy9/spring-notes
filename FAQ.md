---
---
# Frequently Asked Questions

## Why are public keys used for JWT Token decoding?

With JWT, the possession and the use of the key materials are exactly the same as any other contexts where cypher operations occur.
```
- For signing:

The private key is owned by the issuer and is used to compute the signature.

The public key can be shared with all parties that need to verify the signature.

- For encryption:

The private key is owned by the recipient and is used to decrypt the data.

The public key can be shared to any party that want to send sensitive data to the recipient.
```

The issuer of the token (the authentication server) has a private key to generate signed tokens (JWS). These tokens are sent to the clients (an API server, a web/native application...). The clients can verify the token with the public key. The key is usually fetched using a public URI.

In the demo, we implemented a Decoder using a [NimbusJwtDecoder](https://docs.spring.io/spring-security/site/docs/current/api/org/springframework/security/oauth2/jwt/NimbusJwtDecoder.html#withPublicKey(java.security.interfaces.RSAPublicKey)) and according to the documentation,  the *withPublicKey* method is used to *validate JWTs*. Hence we use public Key to do the validation in the JwtDecoder method.

## Can UserDetails be stored as lists?

It can be stored as lists, but the UserDetailsManager classes we used, doesn't seem to have a constructor which can take [*List*](https://docs.oracle.com/javase/8/docs/api/java/util/List.html).
