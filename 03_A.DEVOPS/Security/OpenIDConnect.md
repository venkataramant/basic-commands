							OpenID Connect
Introduction
	Rigidly defined
	Strictly Structured JWTs
	Numerous Extentions

	ID Tokens (represents User Profile)
	Userinfo endpoint
	No Client Credentials

Sample ID token (Decoded)

	{
		"iss" : "http://myserver.tvr.learn",
		"sub" : "subject123456",
		"aud" : "aud123",
		"nonce": "n-0s6_wafere"
		"exp": "1312281970",
		"iat": "1312281070",
		"given_name": "abc",
		"family_name": "def",
		"gender" :"female",
		"birthdate": "2001-12-31",
		"email": "mymail@none.com",
		"picture" :"http://my.com/mine/my.png"

	}

	OIDC replaces SAML for SSO.

Fundamentals

	Resource Owner  -- Who is authorizing
	Resource Server. -- What is granted access to requester/application
	Grant Type	-- How the requester/applicaiton is asking for access.
	Scope -- What access the application is requesting.
	Authorization Server  -- who the application is asking for access.
	Token -- how the application gets that access. (JWT/Opque String)
	Claims -- the content or information in the token (Authorization info is embedded)
	Resource Server --

OAuth Endpoints
	
		/authorize 
			[RFC 6749 OAuth Core]
			The endpoint that the end user (Resource Owner) interacts with to grant permission for the application to access the resource. It returns an authorization Code or an access token
		/token 
			[RFC 6749 OAuth Core]
			The endpoint to trade an authorization code or refresh for an access token
		/userinfo 
			[OpenID Connect Core]
			The endpoint to retrieve profile information about the authenticated user.
			This returns a spec-defined set of fields, depending on the permissions(Scope) requested.
		
		/.well-known/oauth-authorization-server 
			[RFC 8414 OAuth Authorization Server Metadata Discover]
			The endpoint to retrieve the confi info for the authoriation server
		/introspect 
			[RFC 7662 Token Introspection]
			To learn more about a token.[ Active or not, not revoked within expiration,exp time,scopes..etc]
		/revoke
			[RFC 7009 Token Revocation]
			To deactivate a token.
			Valid for access or refresh tokens.

Grant Type

	Authorization Code [For User Server side]
	Implicit or Hybrid For User Client side]
	Resource Owner Password [Legacy/Transition mode]
	Client Credentials [For Service Accounts]
	Device Code [For User Non-Browser flows]
	Authorization Code with PKCE [For User Client side Latest]

	Authorization
		User/Service
	Include Web Browser or not
	Server side fully or a Client side component


OAuth Scopes
	Scope -a set of permissions

	Examples
	 Github Scopes
		repo
		public_Repo
		repo_deployment
		repo:invite
		write:repo_hook
	 Google Scopes
	 	FQURLs
	   Analytics API : https://www.googleapis.com/auth/analytics
	   App EngineAPI : https://www.googleapis.com/auth/appengine.admin
	   Cloud Biling  : https://www.googleapis.com/auth/cloud-billing
	   Google Chat   : https://www.googleapis.com/auth/chat.delete
	   TagManager API: https://www.googleapis.com/auth/tagmanagers.readonly

	  Okta API Scopes

	  	okta.apps.manage
	  	okta.apps.read
	  	okta.authorizationServers.manage
	  	okta.authorizationServers.read

	 OpenID Connect Scopes
	 	openid
	 	profile
	 	email
	 	address
	 	phone

OAuth Playground
	
	developer.google.com/oauth/playground
		Authorize APIs
		Exchange authorization code for tokens
		Configure Request to API

OAuth 2.0 Tokens
	An access token is a string representing an authorization issued to the client. The string is usuallly opque to the client. Tokens represent specific scopes and durations of access, granted by the resource owner, and enforced by the resource server and authorization server.

	A refresh token is a string representing the authorization granted to the client by the resource owner. The token denotes an identifier used to retrieve the authorization information.

	JSON Web Token (JWT)
		Full of Authorization and Profile data.
	ID Token
		The primary extention that OpenID Connect makes to OAuth 2.0 to enable End-Users to be Authenticated is the ID Token datastructure.
		
		The ID Token is a security token that contains Claims about Authentication of an End-User by an Authorization Server when using a Client,and potentially other requested Claims. The ID Token is represented as a JSON Web Token (JWT).

Validating JWTs
	Signing Keys (Public key of sender)

	access_token
		header_jwt.payload_jwt.signature

		header_jwt has information which algorithm to use to fetch signature of paypload.
		Use Public key of Authorization Server and access_token  using algorithm in header_jwt, compare with signature portion to know the validity of the message.
	https://jwt.io
Handling Tokens Safely

	Tokens(Access/Refresh) are credentials.
	Secure Cookies
	Don't embed sensitive data.

	Access Token
		Read-Only,low-risk data: long expiration
		Read-Only, sensitive data: shorter expiration
		Write, low/sensitive data, shorter-expiration

	Revoke Tokens
		lower expiration
		Refresh Token
			retrieve new access tokens

OAuth 2.0 -- Authorization Code Flow

	When ever protected resource is accessed, it is redirected to Authorization Server by Web_App ["/authorize"]
	Authorization Server redirect to User with Authentication Prompt.
	User provides Authentication details
	Authorization_Server returns Authorization_Code to Web_App

	Web_App send Authorization_code and Client Secret to ["/token"]
	Authorization_server sends access_token to Web_App
	Web_App access Resource Server with Access Token and gets response.


	User is Subject 	[User Authorization]
	Web_APP is Client	[Client  Authentication]

	> Only the one-time-use authorization code is exposed.
	> The Application never sees the User's credentials.
	> The user never sees the access or refresh tokens.

	


















