````md
# HTTP Basics

## What is HTTP?
HTTP (HyperText Transfer Protocol) is an application-layer protocol used for communication between web browsers and web servers.

HTTP works on a client-server model:
- Client sends a request
- Server sends a response

HTTP is stateless, meaning the server does not remember previous requests.

Cookies help websites remember user information such as:
- Logins
- Sessions
- Preferences

---

# What Happens When You Open a Website

1. You type a website address in the browser.
2. The browser sends an HTTP request to the server.
3. The server sends back an HTTP response.
4. The browser displays the webpage.

---

# Basic HTTP Communication Flow

```text
Browser → HTTP Request → Web Server
Browser ← HTTP Response ← Web Server
````

---

# HTTP Request Methods

## GET

Retrieves data from the server.

## HEAD

Same as GET but only returns headers without the response body.

## POST

Sends data to the server, usually creating or modifying data.

## PUT

Replaces an existing resource with new data.

## DELETE

Removes a resource from the server.

## CONNECT

Creates a connection tunnel to the server.

## OPTIONS

Shows available communication methods for a resource.

## TRACE

Tests the path taken by a request.

## PATCH

Partially updates a resource.

---

# HTTP Response Status Codes

HTTP status codes show whether a request was successful or not.

## Status Code Classes

| Range   | Meaning                 |
| ------- | ----------------------- |
| 100–199 | Informational responses |
| 200–299 | Successful responses    |
| 300–399 | Redirection messages    |
| 400–499 | Client error responses  |
| 500–599 | Server error responses  |

---

# Important Status Codes

## 200 OK

The request was successful.

## 301 Moved Permanently

The resource URL has permanently changed.

## 302 Found

The resource URL has temporarily changed.

## 403 Forbidden

Access to the resource is denied.

## 404 Not Found

The requested resource could not be found.

## 500 Internal Server Error

The server encountered an unexpected problem.

---

# HTTP Headers

Headers provide additional information during HTTP communication.

---

## Cookie (Request Header)

Used to send session data from the browser to the server.

Example:

```http
Cookie: sessionid=abc123
```

Important for:

* Session tracking
* Authentication

Security Note:
If attackers steal cookies, they may hijack user sessions.

---

## Set-Cookie (Response Header)

Used by the server to create cookies in the browser.

Example:

```http
Set-Cookie: sessionid=abc123
```

Important cookie attributes:

* `HttpOnly` → Prevents JavaScript access
* `Secure` → Sends cookie only over HTTPS

---

## Authorization (Request Header)

Used to send authentication credentials or tokens.

Example:

```http
Authorization: Bearer eyJhbGci...
```

Commonly used with:

* JWT
* APIs
* Access tokens

---

## Content-Type (Request/Response Header)

Specifies the format of the data being sent.

Examples:

```http
Content-Type: application/json
```

```http
Content-Type: application/x-www-form-urlencoded
```

Important for:

* APIs
* Request manipulation
* Burp Suite testing

---

## User-Agent (Request Header)

Identifies the browser or client making the request.

Example:

```http
User-Agent: Mozilla/5.0
```

Servers may use it to:

* Detect browser type
* Customize responses
* Track client information

---

# Cookies

## Creating Cookies

The server creates cookies using the `Set-Cookie` header.

Example:

```http
Set-Cookie: sessionid=abc123
```

---

## Sending Cookies

The browser sends cookies back using the `Cookie` header.

Example:

```http
Cookie: sessionid=abc123
```

---

# Cookie Lifetime

## Permanent Cookies

Remain stored until expiration.

Example:

```http
Set-Cookie: id=a3fWa; Max-Age=2592000
```

---

## Session Cookies

Deleted when the browser session ends.

Do not use:

* `Expires`
* `Max-Age`

---

## Removing Cookies

A cookie can be deleted using:

```http
Set-Cookie: id=a3fWa; Max-Age=0
```

---

# Cookie Security

## Secure Attribute

Cookie is only sent over HTTPS.

Example:

```http
Set-Cookie: id=a3fWa; Secure
```

---

## HttpOnly Attribute

Prevents JavaScript access to cookies.

Example:

```http
Set-Cookie: id=a3fWa; HttpOnly
```

Security Benefit:
Helps protect against XSS attacks.

---

# Important Cookie Security Notes

* Stolen session cookies can allow account hijacking
* Authentication cookies should use:

  * `Secure`
  * `HttpOnly`
* Session cookies should be regenerated after login

---

# Cookie Scope

## Domain Attribute

Defines which domains can receive the cookie.

Example:

```http
Set-Cookie: id=a3fWa; Domain=mozilla.org
```

The cookie will be sent to:

* mozilla.org
* developer.mozilla.org

---

## Path Attribute

Defines which URL paths can receive the cookie.

Example:

```http
Set-Cookie: id=a3fWa; Path=/docs
```

Cookie will be sent to:

* `/docs`
* `/docs/Web`
* `/docs/Web/HTTP`

Cookie will NOT be sent to:

* `/`
* `/docsets`
* `/fr/docs`

Important Note:
`Path` is not a security feature.

---

# Typical HTTP Session

An HTTP session usually has 3 phases:

1. Client establishes connection
2. Client sends HTTP request
3. Server sends HTTP response

HTTP commonly uses TCP.

Default HTTP port:

* 80

Other common ports:

* 8080
* 8000

---

# Structure of an HTTP Request

## 1. Request Line

Contains:

* HTTP method
* Path/URL
* HTTP version

Example:

```http
GET /index.html HTTP/1.1
```

---

## 2. Headers

Provide additional information.

Examples:

* Content-Type
* Cookie
* Authorization
* User-Agent

---

## 3. Request Body (Optional)

Contains additional data.

Mostly used with:

* POST
* PUT
* PATCH

Example:

```json
{
  "username": "admin",
  "password": "1234"
}
```

---

# JWT Basics

## What is JWT?

JWT (JSON Web Token) is used to securely transfer information between a client and server.

Commonly used for:

* Authentication
* Authorization
* APIs

---

# JWT Structure

A JWT has 3 parts:

```text
header.payload.signature
```

## Header

Contains token type and algorithm.

## Payload

Contains user data/claims.

## Signature

Verifies token integrity.

---

# Where JWTs Are Stored

JWTs are commonly stored in:

* Cookies
* Local Storage
* Session Storage

Security Note:
Storing JWTs in Local Storage can be risky because of XSS attacks.

---

# Why JWT is Used

JWT allows stateless authentication.

Widely used in:

* REST APIs
* Single Page Applications (SPA)
* Mobile applications

---

# Important JWT Security Notes

* Stolen JWTs may allow account access
* JWTs should be sent over HTTPS
* Secure and HttpOnly cookies are safer for storing JWTs

```
```
