## Spoofing an Authentication Cookie.md

## Vulnerability Description
The application uses predictable and reversible cookie values to manage authentication. Instead of securely signing or encrypting authentication cookies, it uses a format that can be reverse-engineered and manipulated to spoof other users' identities.

## Steps Taken
  
   ![Step extra](https://github.com/user-attachments/assets/d1695cf7-ca43-495a-8a00-b1b1e487ff4a)

1. Logged in using valid credentials `webgoat:webgoat` to retrieve an authentication cookie.
   ![Step 1](https://github.com/user-attachments/assets/7d6a6315-25ee-4061-a093-9646bccee4fd)

2. Intercepted the login request and extracted the `spoof_auth` cookie.
   ![Step 2](https://github.com/user-attachments/assets/37adcc94-19d4-43ff-8d63-ab7b24fe89f1)

3. Decoded the cookie from base64 format to inspect its content.  
   ![Step 3](https://github.com/user-attachments/assets/fef5a70b-d4a4-441e-b06e-0b2c34e65658)  

4. Identified the decoded string was in hexadecimal format and converted it to text.
   
   ![Step 4](https://github.com/user-attachments/assets/7d047889-d12f-4c18-9f8a-6c4b19edd224)

6. Discovered the username is embedded in reverse (e.g., webgoat becomes "taogbew" reversed and obfuscated).
   ![Step 5](https://github.com/user-attachments/assets/b6167f85-7d12-413d-a7ad-f3264cc5e487)

7. Reversed the username 'tom' into 'mot', appended similar pattern text, converted to hex, then base64 encoded.
   ![Step 6](https://github.com/user-attachments/assets/94a4d32e-46cf-452a-9c98-8424fe4e021a)  
   ![Step 7](https://github.com/user-attachments/assets/43f1b52b-f97e-4c71-bbd1-0ec9bb43dcc1)  
   ![Step 8](https://github.com/user-attachments/assets/3256a6ba-d33d-43bf-a921-fcc1363a9f59)
   
8. Replaced the original cookie with the newly spoofed one and resubmitted the login request.
   ![Step 9](https://github.com/user-attachments/assets/c378ac85-426f-4906-abae-b5720e177e8b)
   
10. Successfully logged in as the user "tom" without valid credentials.
   ![Step 10](https://github.com/user-attachments/assets/4053f070-7d1d-4537-ade2-d9812d6546b0)

## Observed Behavior
The application accepted the manipulated cookie and logged the attacker in as "tom", a user with presumably higher privileges, without requiring their password.

## Risk Rating
**High** – This vulnerability allows an attacker to bypass authentication entirely, impersonate any user, and potentially access sensitive information or administrative functions.

## Remediation Recommendation
Implement proper authentication cookie handling using:
- Signed cookies with HMAC to verify authenticity
- Encrypted cookie values to prevent readable or tamperable content
- Regenerating sessions upon login and validating cookies server-side

## References
- OWASP: [Authentication and Session Management](https://owasp.org/www-project-top-ten/2017/A2_2017-Broken_Authentication)
- OWASP: [Cookie Security](https://owasp.org/www-community/controls/SecureCookieAttribute)
"""
