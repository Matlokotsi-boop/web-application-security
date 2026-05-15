# Authentication Basics

## What is Authentication?

Authentication is the process of verifying the identity of a user or system.

It answers the question:

> "Who are you?"

Authentication is commonly used in:
- Login systems
- APIs
- Banking systems
- Web applications

---

# Authentication Process

Basic authentication flow:

```text
User → Login Request → Server
User ← Authentication Result ← Server
```

---

# Common Authentication Methods

## Password-Based Authentication

The user provides:

* Username
* Password

The server checks whether the credentials are correct.

---

## Multi-Factor Authentication (MFA)

Requires additional verification besides a password.

Examples:

* OTP codes
* Authenticator apps
* Fingerprints

Security Benefit:
Even if a password is stolen, attackers may still fail to access the account.

---

## Token-Based Authentication

After successful login, the server issues a token.

Examples:

* JWT (JSON Web Token)
* Access Tokens

The client sends the token with future requests.

Example:

```http
Authorization: Bearer eyJhbGci...
```

Commonly used in:

* APIs
* Single Page Applications (SPA)
* Mobile applications

---

# Sessions

A session allows the server to remember authenticated users.

After login:

1. Server creates a session
2. Session ID is generated
3. Session ID is stored in a cookie
4. Browser sends the cookie with future requests

Example:

```http
Cookie: sessionid=abc123
```

---

# Cookies in Authentication

Cookies are commonly used to:

* Maintain login state
* Store session identifiers
* Track authenticated users

Important security attributes:

## Secure

Cookie is only sent over HTTPS.

Example:

```http
Set-Cookie: sessionid=abc123; Secure
```

---

## HttpOnly

Prevents JavaScript from accessing the cookie.

Example:

```http
Set-Cookie: sessionid=abc123; HttpOnly
```

Security Benefit:
Helps reduce the risk of session theft through XSS attacks.

---

# JWT (JSON Web Token)

JWT is commonly used for stateless authentication.

JWT structure:

```text
header.payload.signature
```

JWTs are often stored in:

* Cookies
* Local Storage
* Session Storage

Security Note:
Storing JWTs in Local Storage may increase XSS risk.

---

# Authentication Security Risks

Weak authentication systems can lead to:

* Account takeover
* Unauthorized access
* Session hijacking
* Credential theft

---

# Common Authentication Vulnerabilities

## Weak Passwords

Users may choose:

* Short passwords
* Common passwords
* Reused passwords

Examples:

* 123456
* password
* admin

---

## Brute Force Attacks

Attackers repeatedly try many password combinations until successful.

Protection methods:

* Rate limiting
* Account lockout
* MFA

---

## Credential Stuffing

Attackers use leaked username/password combinations from previous data breaches.

---

## Session Hijacking

Attackers steal session cookies to impersonate users.

Example:
If attackers steal:

```http
Cookie: sessionid=abc123
```

They may gain access to the victim's account.

---

## Broken Authentication

Occurs when authentication systems are poorly implemented.

Examples:

* Weak session management
* Predictable session IDs
* Missing MFA
* Improper logout handling

---

# Authentication Best Practices

## Strong Password Policies

Encourage:

* Long passwords
* Complex passwords
* Password managers

---

## Use HTTPS

Authentication data should always be transmitted securely.

---

## Enable MFA

Adds additional protection against stolen credentials.

---

## Secure Session Management

Use:

* Secure cookies
* HttpOnly cookies
* Session expiration
* Session regeneration after login

---

## Protect Against Brute Force

Common protections:

* Rate limiting
* CAPTCHA
* Temporary account lockouts

---

# Authentication in APIs

APIs commonly use:

* JWT
* OAuth
* Bearer tokens

Authentication credentials are often sent using:

```http
Authorization: Bearer token_here
```

---

# Important Security Notes

* Authentication verifies identity
* Authorization determines permissions
* Stolen session tokens can lead to account compromise
* Weak authentication systems are common attack targets
* Secure authentication is critical in web application security
