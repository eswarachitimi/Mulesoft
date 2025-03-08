### Why we use identity management?

You can configure identity management to set up users for Single sign-on.

Following are below SSO Standards -

- Open ID connect
- SAML 2.0
- Salesforce
- Open AM
- OKTA
- Ping Federate

### Why we use client management?

With the help of client management you can configure external client provider to authorize client applications. As a API owner you  can also apply the OAUTH policy to authorize client to access your apis to use the OAUTH policy you need an OAUTH provider.

Mulesoft provides below options to configure the OAUTH providers-

- Open AM
- Ping Federate
- OpenID Connect Dynamic Client Registration
  
### How many ways we can ensure data and API security?

- Multi-factor Authentication
- Token-based authentication
- Digital signature
- Public key cryptography
- Digital certificate

## What is OATH 2.0 dance?

The OAuth 2.0 dance is the authentication process performed by the Mule OAuth 2.0 provider, API, and client application

## What are the Grant type in OAUTH 2.0?

- AUTHORIZATION_CODE
- IMPLICIT
- RESOURCE_OWNER_PASSWORD_CREDENTIALS
- CLIENT_CREDENTIALS

## What are keystore and truststore?

- In SSL handshake purpose of trustStore is to verify credentials and the purpose of keyStore is to provide credential -
  
  > keyStore stores private key and certificates corresponding to there public keys and require if you are SSL Server or SSL requires client authentication.
  
  > TrustStore stores certificates from third party, your Java application communicate or certificates signed by CA(certificate authorities like Verisign, Thawte, Geotrust or GoDaddy) which can be used to identify third party
More info on creating KeyStore and TrustStore
