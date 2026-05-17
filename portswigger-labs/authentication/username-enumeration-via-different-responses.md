````md id="a9f2k1"
# Username Enumeration via Different Responses

## Lab Information

- **Platform:** PortSwigger Web Security Academy
- **Tool Used:** Burp Suite Community Edition
- **Difficulty:** Apprentice
- **Category:** Authentication

---

# Objective

Exploit inconsistent response lengths to:
1. Enumerate a valid username
2. Brute force the password
3. Gain access to the target account

---

# Vulnerability Description

The application returns different response lengths depending on whether:
- the username exists
- the password is correct

This behavior allows attackers to identify valid usernames and later brute force passwords.

In Burp Suite Intruder, the difference can be observed in:
- Response length
- Status codes

---

# Attack Flow

```text
Attacker → Username Enumeration → Valid Username Found
Attacker → Password Brute Force → Account Access
````

---

# Step 1 — Username Enumeration

## Process

1. Intercept the login POST request using Burp Suite.
2. Send the request to Intruder.
3. Set the `username` parameter as the payload position.
4. Use a username wordlist.
5. Start the attack.
6. Sort responses by `Length`.

---


## Result

Username `root` returned a response length of `3354`.

Other usernames returned:

* `3352`

This confirmed that:

```text id="s0g8mn"
root
```

is a valid username.

---

# Step 2 — Password Brute Force

## Process

1. Set username to:

```text id="g8m3yw"
root
```

2. Set the `password` parameter as the payload position.
3. Use a password wordlist.
4. Start the attack.
5. Sort responses by:

* Status
* Length

---

# Result

Password:

```text id="j6n0cz"
andrew
```

returned:

* Status Code: `302`
* Response Length: `186`

Other passwords returned:

* Status Code: `200`

The `302` redirect indicated successful authentication.

---

# Valid Credentials

```text id="w2x7ke"
Username: root
Password: andrew
```

Using these credentials successfully solved the lab.

---

# Why the Vulnerability Exists

The application exposes different responses depending on whether usernames are valid.

Attackers can analyze:

* Response lengths
* Response messages
* Status codes

This allows valid usernames to be identified before brute forcing passwords.

---

# Impact

## Username Enumeration

Attackers can identify valid accounts.

## Account Takeover

Weak passwords may allow attackers to compromise accounts.

---

# Remediation

## Consistent Responses

Return identical response lengths and messages for all failed logins.

---

## Generic Error Messages

Use:

```text id="cv3n4h"
Invalid username or password
```

for all authentication failures.

---

## Rate Limiting

Prevent rapid automated login attempts.

---

## CAPTCHA

Reduce automated brute-force attacks.

---

## Account Lockout

Temporarily lock accounts after repeated failed attempts.

---

# Key Takeaways

* Authentication responses should remain consistent.
* Response lengths can leak sensitive information.
* Burp Suite Intruder is useful for enumeration attacks.
* Weak authentication mechanisms increase attack surface.
* Generic error handling is important for secure authentication systems.

```
```
