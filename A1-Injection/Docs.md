# (A1) Broken Access Control

### Vulnerability Description
The application uses predictable session tokens (`hijack_cookie`), allowing attackers to brute-force valid session IDs. This enables unauthorized access to other users’ sessions. Poor randomness in token generation leads to session hijacking.


---


### Steps Taken

1. **Initial Observation**  
   Navigated to the "Hijack a Session" WebGoat module to understand the session-based access control issue.  
     <img width="909" alt="a1_1" src="https://github.com/user-attachments/assets/30b7c71a-267d-465e-adaf-22f176300373" />

2. **Captured Login Request** 
   login to capture a request for analyzing.
     <img width="923" alt="Screenshot 2025-03-29 022622" src="https://github.com/user-attachments/assets/fb3d01d5-fcee-41d7-8d8b-84d9d527d8cf" />
  
3. **Setup Request in Burp Suite**  
   Sent the intercepted request to Repeater, removed the hijack_cookie, and resent it to observe the behavior. A new cookie was issued by the server.  
     <img width="660" alt="a1_2" src="https://github.com/user-attachments/assets/e1450eff-6f3b-4172-a49e-d7b83f3808df" />

4. **Observed Cookie Pattern**  
   Repeated the login request multiple times. The hijack_cookie value was updated for each request and appeared sequential with slight variation. These values were saved for analysis.  
     <img width="657" alt="a1_3" src="https://github.com/user-attachments/assets/7a849a30-3ff5-4cd5-b4b9-ad0ea5686ea5" />

5. **Identified Predictable Patterns**  
   Identified a predictable pattern in hijack_cookie values. While mostly sequential, some values were skipped, indicating possible valid sessions..  
     <img width="232" alt="a1_4" src="https://github.com/user-attachments/assets/60ca4c9d-763b-4020-a29f-f5bc96dc7262" />

6. **Brute Force via Intruder**  
  sent a new request in Intruder using one of the skipped session cookies and brute-forced the timestamp portion to find a valid session.  
     <img width="659" alt="a1_5" src="https://github.com/user-attachments/assets/fcc6df0f-35e6-46d9-ab4d-b0cd02ab3e67" />

7. **Successful Session Hijacking**  
   Identified a valid session token, leading to successful unauthorized access.  
     <img width="872" alt="a1_6" src="https://github.com/user-attachments/assets/d7dd092b-d12a-4a3a-9346-723db9e39ade" />

8. **Lesson Completion Confirmed**  
   WebGoat confirmed successful hijacking of a valid session.  
     <img width="454" alt="a1_7" src="https://github.com/user-attachments/assets/32ef45a4-9865-4601-9e3b-783d734176ce" />



---


### Observed Behavior
- WebGoat accepted hijack_cookie with predictable values.
- No rate-limiting or session protection mechanisms were in place.

---

### Risk Rating: **High**
Session hijacking compromises the confidentiality and integrity of user accounts. Exploiting this flaw allows full control over another user's authenticated session.

---

### Remediation Recommendation
- Implement strong, unpredictable session identifiers with high entropy.
- Set secure flags on cookies and apply rate-limiting on session-related endpoints.
- Regularly expire and regenerate session tokens on privilege changes or inactivity.
- Monitor for unusual session access patterns via SIEM/logging.
