# OWASP A7: Identification and Authentication Failures – Insecure Login

## Vulnerability Description

This exercise demonstrates how login credentials can be intercepted when transmitted over an unencrypted channel. Attackers can use tools like packet sniffers or proxy interceptors (e.g., Burp Suite) to capture sensitive data and gain unauthorized access.

---

### ![A](https://github.com/user-attachments/assets/7549c10a-b83c-46f7-88d4-4fd22c20df2c)  

### ![B](https://github.com/user-attachments/assets/2e88bd8d-7e43-42cf-a468-6e0e847f7e7f)  
**Demonstrates a login form vulnerable to credential interception**, encouraging the use of packet sniffers to capture another user's login request.

---

### ![C](https://github.com/user-attachments/assets/aaa8668a-aa6c-4ce4-95b6-ed12e69ec2f6)  
**Captured login credentials (`CaptainJack` / `B1ackPearl`)** using Burp Suite to intercept an insecure HTTP POST request during login, showcasing lack of encryption in WebGoat's Insecure Login lesson.

---

### ![D](https://github.com/user-attachments/assets/83879472-afde-4bff-b633-5802ce3679b6)  
**Success!** Credentials intercepted and reused to gain access, confirming vulnerability in the login process.

---


##  Observed Behavior

- Login form submits credentials via HTTP POST.
- Burp Suite or packet sniffers can easily intercept the request.
- Replaying the request grants access to the target account.

##  Remediation

- Enforce HTTPS using TLS 1.2 or higher for all login forms and authenticated sessions.
- Set HTTP Strict Transport Security (HSTS) headers.
- Avoid transmitting sensitive data over insecure channels.

##  References

- [OWASP A7: Identification and Authentication Failures](https://owasp.org/Top10/A07_2021-Identification_and_Authentication_Failures/)
- [OWASP: Transport Layer Protection Cheat Sheet](https://cheatsheetseries.owasp.org/cheatsheets/Transport_Layer_Protection_Cheat_Sheet.html)
- [Burp Suite Official Documentation](https://portswigger.net/burp/documentation)

---
