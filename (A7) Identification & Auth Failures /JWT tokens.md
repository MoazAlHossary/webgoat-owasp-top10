# OWASP A7: Identification and Authentication Failures – JWT Module

## Vulnerability Description

This module explores the use and misuse of JSON Web Tokens (JWT) for authentication. It covers the token structure, decoding, validation pitfalls, claim tampering, algorithm abuse, and secure token refresh. Through hands-on lessons, it demonstrates how improper implementation of JWTs can lead to serious security vulnerabilities such as privilege escalation and token forgery.

---

### ![A](https://github.com/user-attachments/assets/21402010-e3c1-4494-af66-255d5abd6d8d)  
Introduction to JSON Web Tokens (JWT), highlighting their purpose in secure client-server authentication and the importance of token validation.

### ![B](https://github.com/user-attachments/assets/eb7c2747-62a7-4047-aed1-d5340944c440)  
Visual breakdown of a JWT structure, showing its three components: header, claims (payload), and signature, all base64-encoded for secure transmission.

### ![C](https://github.com/user-attachments/assets/4ee5b263-cd6a-41e2-bce2-63e38a92a4e5)  
JWT claim misuse: common attacks like unauthorized, tampered, excessive, expired, replayed, and manipulated claims, with emphasis on proper validation.

### ![D](https://github.com/user-attachments/assets/62bcfc9b-a63f-4c54-ae69-d89d9fb0657d)  
JWT decoding to reveal user identity embedded in the payload via base64-decoding.

### ![E](https://github.com/user-attachments/assets/ab9755d7-e061-4807-bd77-92092223800c)  
JWT claims inspection, including roles like `ROLE_ADMIN`, `ROLE_USER` shown via decoding tools.

### ![F](https://github.com/user-attachments/assets/95e54410-1754-461b-8366-e7e972aef201)  
Success – JWT decoded and accepted, confirming correct user extraction.

### ![G](https://github.com/user-attachments/assets/c298c844-dfed-41ce-9fa8-7add5f56924d)  
JWT authentication flow: shows token issuance, transmission, and verification.

### ![H](https://github.com/user-attachments/assets/fcfb8e2c-fa20-4efe-ac65-111ed67f916b)  
Assignment overview – escalate privileges from guest to admin by modifying a JWT, focusing on signature verification flaws.

### ![I](https://github.com/user-attachments/assets/fef7b909-e4e8-4d9b-9f0e-382b3439c5fe)  
Access control view – action restricted to admin, target of privilege escalation.

### ![J](https://github.com/user-attachments/assets/77191775-b78d-4801-9a94-60bb20cf0fde)  
Unauthorized JWT attempt – server blocks non-admin token from performing restricted actions.

### ![K](https://github.com/user-attachments/assets/8b59e887-cc12-4995-bbc1-b49cf4d86cf0)  
Decoded JWT showing `admin: false`, highlighting how values can be altered to escalate access.

### ![L](https://github.com/user-attachments/assets/eafd4372-6f3f-45fb-bc2c-dd64b6ca3ed9)  
JWT with `alg: none` – attacker sets algorithm to none and modifies claims to bypass signature verification.

### ![M](https://github.com/user-attachments/assets/04cb6aa5-ea78-4d39-8873-9c219e9415ce)  
Final unsigned JWT crafted, demonstrating privilege escalation without proper validation.

### ![N](https://github.com/user-attachments/assets/134aed18-b6fd-4e52-93d4-f5f5f0517d7b)  
Malformed JWT error, due to incorrect structure (missing periods), emphasizing format strictness.

### ![O](https://github.com/user-attachments/assets/6dddfc12-52fa-4b46-a2ad-04da267a43ce)  
Successful exploit – manipulated JWT passed via cookie (`access_token`) grants admin rights.

### ![P](https://github.com/user-attachments/assets/ddbbfd1f-5c10-4e92-9139-e274f7a7dc48)  
Final success confirmation – exploit complete, admin access achieved.

---

## JWT Implementation Flaws in Depth

### ![Q](https://github.com/user-attachments/assets/1ac35794-d5b7-449f-b5bb-d149f7385c1d)  
Vulnerable library behavior – `alg: none` or `RS256 → HS256` tricks cause insecure JWT parsing.

### ![R](https://github.com/user-attachments/assets/42dba6be-1bf0-426f-9890-4b702f78ae2e)  
Admin claim set to true with `alg: none`, showing successful manipulation and acceptance.

### ![S](https://github.com/user-attachments/assets/67589ae1-d365-4fb4-b6bb-93e931210279)  
Code-level vulnerability – insecure `parse` method lets unsigned JWTs pass without validation.

### ![T](https://github.com/user-attachments/assets/e991af74-b3d3-4b8a-a699-97da62b330d6)  
Only signature removed – token still accepted due to incorrect parsing logic (`parse` vs `parseClaimsJws`).

### ![U](https://github.com/user-attachments/assets/60f721ef-5da6-43bd-bcad-53e240c98581)  
Lesson wrap-up – highlights misuses beyond `alg: none`, recommends Paseto for safer token practices.

---

## Token Refresh & Session Management

### ![V](https://github.com/user-attachments/assets/7700d211-cbe0-4c1f-b703-0dc1d32063b6)  
Access vs Refresh tokens – explains lifecycle, usage, security considerations, and token renewal risks.

---

## Advanced JWT Claim Exploits

### ![W](https://github.com/user-attachments/assets/89584f94-3b11-4982-8eae-2e0c828b1640)  
JWT claim misuse summary – unauthorized roles, expiration tampering, and replay risks explained with mitigation tips.

### ![X](https://github.com/user-attachments/assets/4ee19d97-64ac-4679-b10c-33753504700c)  
JWT header `jku` abuse – attackers specify malicious key URLs to forge trusted tokens unless whitelisted.

---


## Observed Behavior

- Tokens with altered claims (e.g., `admin: true`) were accepted
- Tampered tokens passed validation when signature checking was bypassed
- JWTs signed with `alg: none` or no signature were accepted as valid
- Admin-only actions were completed using forged tokens
- Refresh tokens were used without proper checks on origin or scope

---

## Remediation

- Always validate JWT signatures using secure libraries (`parseClaimsJws`)
- Reject any tokens with `alg: none` or an unsupported algorithm
- Use algorithm whitelisting and enforce key-based verification (e.g., RS256 only)
- Never trust data in JWT payload without additional server-side authorization checks
- Disable dynamic key resolution from headers like `jku` unless whitelisted
- Rotate keys regularly and minimize token lifespans (short TTLs)
- Prefer using [Paseto](https://paseto.io) if JWT security is hard to enforce correctly

---

## References

- [OWASP A7: Identification and Authentication Failures](https://owasp.org/Top10/A07_2021-Identification_and_Authentication_Failures/)
- [JWT.IO – Learn and Debug JSON Web Tokens](https://jwt.io/)
- [CVE-2015-9235](https://nvd.nist.gov/vuln/detail/CVE-2015-9235)
- [Paseto Project](https://paseto.io/)
- [JWT Claim Injection – PortSwigger](https://portswigger.net/web-security/jwt)
