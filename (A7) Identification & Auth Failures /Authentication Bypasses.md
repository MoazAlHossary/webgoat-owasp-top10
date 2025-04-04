# OWASP A7: Identification and Authentication Failures

## Vulnerability Description

Authentication bypass vulnerabilities occur when authentication mechanisms can be tricked or circumvented. In WebGoat A7, users explore how flawed implementations—like poorly validated security questions or hidden fields—can lead to unauthorized access.

---

### ![A](https://github.com/user-attachments/assets/066efe17-ffa5-4878-ad93-b09c8bd21ea8)  
**Overview of common authentication bypass techniques:** hidden inputs, parameter removal, and forced browsing in WebGoat A7.

---

### ![B](https://github.com/user-attachments/assets/6da8c11f-6d54-4d9f-92ba-d71e333b0a0e)  
**Demonstrates bypassing 2FA password reset** by removing security question parameters using a proxy tool.

---

### ![C](https://github.com/user-attachments/assets/df099427-26fa-46e3-af79-880a69c50bc6)  
**WebGoat scenario illustrating fallback verification** using security questions when 2FA fails on an unrecognized device.

---

### ![D](https://github.com/user-attachments/assets/4dcb1a4a-7733-44d4-b8ad-6761856ae3c4)  
**Bypassing account verification** by sending crafted parameters `secQuestionA` and `secQuestionB` with arbitrary values, tricking the system into accepting the input and completing the lesson.

---

### ![E](https://github.com/user-attachments/assets/95203d8a-be74-4645-9e90-8f96255cd5ca)  
**Success!** The system allows a password change without actually verifying identity.

---


##  Observed Behavior

- Authentication steps can be bypassed by removing or tampering with parameters like `securityQuestion1`.
- Arbitrary values passed to `secQuestionA` and `secQuestionB` lead to full access without proper verification.
- The application displays a success message and allows password changes post-bypass.

##  Remediation

- Avoid relying on security questions as a sole fallback method—they are often guessable or found via social engineering.
- Implement strong input validation and server-side checks for authentication tokens and session state.
- Use secure, multi-factor authentication without fallback to weak alternatives unless equally secure.

##  References

- [OWASP A7: Identification and Authentication Failures](https://owasp.org/Top10/A07_2021-Identification_and_Authentication_Failures/)
- [2FA Bypass Blog Example (Paypal)](https://henryhoggard.co.uk/blog/Paypal-2FA-Bypass)
- [OWASP WebGoat Project](https://owasp.org/www-project-webgoat/)


