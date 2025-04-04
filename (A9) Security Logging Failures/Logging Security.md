# Logging Security

## Vulnerability Description

Logging security failures occur when applications do not properly validate, sanitize, or protect the information being logged. This can lead to log injection, spoofing, information leakage, and missed detections of security incidents. Attackers may exploit these flaws to mislead log monitoring systems, cover their tracks, or extract sensitive information.

Logging should avoid recording sensitive data such as passwords, API keys, or PII. Improper logging may also allow attackers to inject malicious log entries or cause confusion in audit trails.

---

## Step-by-Step Documentation with Screenshots

### 1. **Concept and Goals**
![a](https://github.com/user-attachments/assets/6bc67685-654b-49c4-9330-5a5b5162eabb)
This section explains the purpose of logging and its goals in application security.

### 2. **Log Spoofing Demo**
![b](https://github.com/user-attachments/assets/4403c4ea-9627-407a-b5ad-933e884c9783)
Here, user input is reflected in the logs directly, enabling spoofing through controlled input like "admin".

### 3. **Logging Practices and Risk**
![c](https://github.com/user-attachments/assets/b90fc260-6812-4cc7-9a4e-6880d4badc71)
Highlights risks like log tampering, storing sensitive data, and failing to sanitize sources.

### 4. **Admin Credentials in Logs**
![d](https://github.com/user-attachments/assets/1908b0d7-5c82-449f-b4af-91f7c7b576b5)
Admin password is logged in Base64 format during app initialization, representing an info leak.

### 5. **Base64 Decoding**
![e](https://github.com/user-attachments/assets/e7ca168c-3afe-4229-8db0-54fde50fcd94)
Decoded the Base64 password using an online tool revealing the actual UUID format secret.

### 6. **Login Success**
![f](https://github.com/user-attachments/assets/ae476688-ef59-4dd3-87ce-e067e1268aff)
Used the decoded password to login as the "Admin" user, completing the challenge.

### 7. **Advanced Logging Use**
![g](https://github.com/user-attachments/assets/a2119d7e-8391-4ffa-b042-ce948763a7c8)
Logging can also support fraud detection, audit trails, and system monitoring if configured securely.

### 7. **More about logging in (2)**
![g](https://github.com/user-attachments/assets/726d9273-3b29-4481-b114-e8f8cd21ef78)


---


## Observed Behavior

- **Log Injection**: The application logs user-supplied input directly, allowing attackers to insert log entries that appear legitimate.
- **Base64 Leakage**: Admin password was exposed in logs during application startup, though encoded in Base64.
- **Log Decoding**: The leaked Base64 string could be decoded to a UUID format password, allowing admin login.
- **No Input Validation**: Inputs like `admin` are not sanitized before logging, making spoofing easier.
- **Improper Log Protection**: Sensitive authentication credentials were found in the logs without encryption or obfuscation.

---

## Remediation

- **Input Sanitization**: Always sanitize user inputs before logging them to prevent injection and spoofing.
- **Avoid Logging Sensitive Data**: Passwords, secrets, tokens, and PII must never be logged.
- **Log Access Control**: Secure logs with access permissions to restrict who can view and modify them.
- **Log Monitoring**: Employ centralized logging and SIEM tools to detect anomalies and attack indicators.
- **Audit Logs Separation**: Separate application, audit, and security logs to enhance clarity and control.
- **Mask or Hash Sensitive Fields**: If sensitive data must be referenced, use irreversible hashes or masking.

---

## References

- [OWASP Logging Cheat Sheet](https://cheatsheetseries.owasp.org/cheatsheets/Logging_Cheat_Sheet.html)
- [GDPR article at Wikipedia](https://en.wikipedia.org/wiki/General_Data_Protection_Regulation)
