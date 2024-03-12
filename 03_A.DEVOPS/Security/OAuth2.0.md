Authentication (AuthN)
		Who are you?
Authorization (Authz)
		What can you do?

OAuth 2.0
	OAuth2.0 is an authorization framework.
	Loose operating agreement, not a contract. (Defines the boundaries). It gives flexibility for extensions.
	
		Loosely Defined
		Unstructed tokens
		Numerious extensions
		Access and refresh tokens
		Authorize and token end points
		Authorization Code, Implict Resource Owner Password and Client Credentials


OpenID Connect OICD
	OpenID Connect is an OAuth 2.0 extension putting function and form to a user's profile information. It is a special case of OAuth2.0
	It provides a standard way to request and share profile data, depends on Json Web Tokens (JWTs)

Json Web Token (JWT)
		iss (Issuer)
		iat (Issued At)
		sub (Subject)
		aud (Audience)
		exp (Expriations)
	JWTs are encoded, not encrypted.

	Json Web Encryption (JWE)


RFC 7662 Token Introspection.

	Examines a token to describe its contents.
		Useful for opaque tokens
		Describes if the token is active or not.

RFC 7009 Token Revocation
	Revokes (cancels) a token via API

RFC 8636 Auth Code with PKCE
	Protecting client-side flows
	It replaces the implict grant type.

RFC 8693 Token Exchange (Impersonation)
	Introduces an approach for trading or exchanging tokens on behalf of another user or service, aka "delegation"

RFC 8414 Authorization Server Metadata

PostMan/Insomnia

OAuth Server
	https://oauth2.thephpleague.com (PHP Based)
		Authorization code grant
		Implicit grant
		Client credentials grant
		Resource owner password credentials grant
		Refresh grant
	https://developers.google.com/oauthplayground


	https://developer.okta.com (API Access Management)

Token Introspection Extension
	https://jwt.io