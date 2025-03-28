## A1 – Broken Access Control (IDOR – Insecure Direct Object Reference)

### Vulnerability Description
The application exposes internal object references such as `userId`, which can be manipulated to access other users' data. This results in unauthorized access due to insufficient access control validation.

---

### Steps Taken

1. **Authenticate First, Abuse Authorization Later**  
   Logged in using known test credentials (`user: tom`, `pass: cat`) and accessed personal profile information.  
   ![a11_1](https://github.com/user-attachments/assets/da055ba6-09b3-4eb1-8c87-d08d7636a338)

2. **Observing Differences & Behaviors**  
   Intercepted the profile request using Burp Suite and reviewed the raw JSON. Noted that `userId` and `role` fields were returned by the backend but not rendered in the UI.  
   ![a11_2](https://github.com/user-attachments/assets/5d169663-0e08-46ad-b166-c8a0f1882211)  
   ![a11_3](https://github.com/user-attachments/assets/68211eb7-b46a-4c9e-b1b8-aa7d9f811824)

   Submitted `userId` and `role` as the hidden attributes revealed only through the raw server response.  
   ![a11_4](https://github.com/user-attachments/assets/8d9a181d-c7eb-4716-958b-5249ed3edb35)

3. **Guessing & Predicting Patterns**  
   Using the known `userId` from previous task, navigate to `/WebGoat/IDOR/profile/2342384` and confirmed the profile was accessible directly.  
   ![a11_6](https://github.com/user-attachments/assets/b9a64de5-a725-4606-9ce0-339c86f1bb25)  
   ![a11_7](https://github.com/user-attachments/assets/7810df99-0da5-4800-802b-65762304544e)

5. **Playing with the Patterns**  
   ![a11_8](https://github.com/user-attachments/assets/e9ade473-45c9-4653-bf0c-739d8156c479)

 **Captured IDOR via Burp**  
   Manually intercepted the request via Burp Suite while viewing the profile.  
   ![a11_9](https://github.com/user-attachments/assets/7cb02362-747e-4db7-91e3-acdd7c9ec1c0)

 **Brute-Forced IDs Using Burp Intruder**  
   Used Intruder to automate testing of userId values from `2342384` to `2342399`, confirming multiple unauthorized profile accesses.  
   ![a11_10](https://github.com/user-attachments/assets/c9a180a4-8181-4a66-907d-fcb9c4758b82)
   <img width="872" alt="a11_11" src="https://github.com/user-attachments/assets/3ffebeb6-6461-4640-898e-1faacb586c06" />


 **Confirmed Successful Unauthorized Access**  
   The server responded with profile information for other users, proving IDOR vulnerability via brute-forced IDs.  
<img width="1274" alt="a11_12" src="https://github.com/user-attachments/assets/90937f2c-3011-4bac-8b54-04bb7efa0d5c" />





---

### Observed Behavior
- Server responds with user profile data when provided a direct object reference (`userId`) in the URL.
- No access control is enforced to verify the requesting user owns the referenced object.

---

### Risk Rating
**High** – Enables unauthorized data access and potential privilege escalation across user accounts.

---

### Remediation Recommendation
- Do not expose internal identifiers like `userId` in URLs or client-side code.
- Enforce strict access control checks on every resource access.
- Use indirect object references or UUIDs combined with server-side authorization validation.

---

### References
- [OWASP Insecure Direct Object Reference Prevention Cheat Sheet](https://cheatsheetseries.owasp.org/cheatsheets/Insecure_Direct_Object_Reference_Prevention_Cheat_Sheet.html)
- [OWASP Top 10: A01:2021 – Broken Access Control](https://owasp.org/Top10/A01_2021-Broken_Access_Control/)
- [OWASP Testing Guide: IDOR](https://owasp.org/www-project-web-security-testing-guide/stable/4-Web_Application_Security_Testing/07-Input_Validation_Testing/10-Testing_for_Insecure_Direct_Object_References.html)
