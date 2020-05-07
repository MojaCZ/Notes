# WEB TECHNOLOGIES

[JavaScript](JavaScript.md)

[TypeScript](TypeScript.md)

[Angular](Angular.md)

[NodeJS](NodeJS.md)

[CSS](CSS.md)

[SCSS](SCSS.md) (newer) - can compile CSS code (if I just change .css to .scss it is ok)
SASS (older)

[REST API](#REST-API)

[WEB AUTHENTICATION](#WEB-AUTHENTICATION)

## REST API
REST - REpresentation State Transfer (style of software architecture)
RESTFUL - follows ALL the principles of REST application

REST principles:
* should be stateless
* should access all the resources from the server using only URI
* does not have inbuilt encription
* does not have session
* uses only HTTP protocol
* for operations should use HTTP verbs such as get, post, put and delete
* should return result in JSON or XML

Web API - Application Programming Interface
- interface for web server or web browser.
- allows to communicate one piece of software to another

REST API - the way application communicate to a server
example `https://graph.facebook.com/youtube` will return JSON object

## WEB AUTHENTICATION
Authentication (verifying identity - `401 Unauthorized`) and authorization (verifying permissings - `403 Forbidden`)
Stateful (using session or cookie) vs stateless (using token such as JWT / OAuth / other)

Web Authentication API Methods:
* `navigator.credentials.create()` when used with the publicKey option, creates new credentials, either for registering a new account or for associating a new asymmetric key pair credentials with an existing account.
* `navigator.credentials.get()` when used with the publicKey option, uses an existing set of credentials to authenticate to a service, either logging a user in or as a form of second-factor authentication.

### Sessions and Cookies
Flow:
* user submits login credentials (email, pw)
* server varifies the credentials against DB
* server creates a temporary user session
* server issues a cookie with a sessionID
* user sends the cookie with each request
* server validates it against the session store and grants access
* when user logs out, server destroys the session & clears the cookie

### Tokens
Tokens are not stored on server, only client have it stored (is stateless).
Tokens can carry only a id or other generated string, or it can contain payload (actual information)
Flow:
* user submits login credentials (email, pw)
* server verifies the credentials against the DB
* server generates a temporary **token** and embeds user data into it
* server responds back with the token (in body or header)
* user stores the token in client storage
* user sends the token along with each request
* server verifies the token & grants access
* when user logs out, token is cleared from client storage

JWT (JSON Web Tokens)
* open standard for authorization and info exchange
* contain: header (meta), payload (claims) and signature, all delimited by `.`
* when the token is encoded, it shows the JSON structure, for example `atob(eyJhbGciOiJI....)` will encode into `"{"alg":"HS256", "typ":"JWT"}"`

## URL & URI
URL - (Uniform Resource Location)
URI - (Uniform Resource Identifier) is a string character that identifies resource
  - scheme: `[//authority]path[?query][#fragment]`
  - authority: `[userinfo@]host[:port]`
  - example: `https://john.doe@www.example.com:123/forum/questions/?tag=networking&order=newest#top` - `scheme://userinfo@host:port/path/?&query#fragment`
URN - (Uniform Resource Name)



API - Application program Interface
  - Contract provided by one piece of software to another
  - structured of request and response

REST - Representation State Transfer
  - Architecture style for designing networked applications
  - usually relies on HTTP

API is messenger, REST helps to format messages

HTTP Methods
* GET
* POST
* PUT - update a specified resource
* DELETE - will delete a specified resource
* HEAD  - same as get but does not return a body
* OPTIONS - returns the supported http methods
* PATCH - update partial resources

example:
* GET `https://mysite.com/api/users`  - for get a list of users
* GET https://mysite.com/api/users/1  - for a specific user (id)
* POST https://mysite.com/api/users - for adding user (same URL, different method then GET)
* PUT https://mysite.com/api/users/1 or https://mysite.com/api/users/update/1
* DELETE https://mysite.com/api/users/1 or https://mysite.com/api/users/delete/1

##Authentication
