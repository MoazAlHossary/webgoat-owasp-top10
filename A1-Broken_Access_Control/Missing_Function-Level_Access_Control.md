### Vulnerability Description
Some functionalities in the application are only hidden using client-side controls (e.g., CSS or JavaScript) rather than proper server-side authorization. This allows users to access unauthorized functions by directly navigating to hidden endpoints.

---


### Steps Taken
   ![l.png](https://github.com/user-attachments/assets/0d59eebf-8538-489d-b051-2471324b8688)

1. **Located Hidden Functionality**  
   Reviewed the UI and source code using browser developer tools. Found hidden menu items `Users` and `Config` which were obscured via CSS classes like `hidden-menu-item`.
   ![c.png](https://github.com/user-attachments/assets/8795840d-83fb-4199-9ff4-3a73dbf410b2)  
   ![a12_2.png](https://github.com/user-attachments/assets/c3e30bc6-f78d-4055-a71b-68602f7d6090)  

3. **Confirmed Access to Hidden Items**  
   Submitted the hidden items `Users` and `Config` in the mission challenge to confirm they were reachable and relevant.
   ![a12_3.png](https://github.com/user-attachments/assets/3d757628-e367-4f81-beb7-f9aed08f07f3)

4. **Tried POST Request to Users Endpoint**  
   Attempted to access the `/access-control/users` endpoint by submitting Jerry’s hash using POST.  
   The first attempt failed with an `Unsupported Media Type (415)` error because the content type was set to `application/x-www-form-urlencoded`.  
   ![a12_4](https://github.com/user-attachments/assets/5b0259c7-8376-487f-b68d-a1df9504bc26)

8. **Updated Content-Type to application/json**  
   Changed the content type to `application/json` and reattempted the POST request.  
   This resulted in a `Bad Request (400)` error, suggesting the server expected a different structure.  
   ![a12_5](https://github.com/user-attachments/assets/2ce124a1-a822-441f-b52c-df86c241f03b)

9. **Switched to GET Method**  
   Realizing POST may not be supported or correct for retrieving data, changed the method to `GET` and appended `?userHash=1234` as a query parameter.  
   Successfully retrieved a list of users including Jerry, with his hash value exposed.  
   ![a12_6](https://github.com/user-attachments/assets/e8d6d3a0-634e-4a6b-98f5-2ee414c85185)

10. **Submitted Jerry’s Hash to Complete the Task**  
    Copied Jerry’s `userHash` (`SVtOlaa+ER+w2eolIVE5/77umhvchsfV8uYbULualtg=`) and submitted it to complete the lesson.  
    Received a confirmation message:  
    **"Congrats! You really succeeded when you added the user."**  
    ![a12_7](https://github.com/user-attachments/assets/8dcd94d8-1123-4bbd-a172-69c1552d166b)

    
---
![image](https://github.com/user-attachments/assets/2c8125fd-9cce-43cf-8657-17f84e93e301)


### Risk Rating
– Functionality hidden only via client-side code can easily be discovered and accessed, leading to sensitive data exposure or unauthorized actions.

---

### Remediation Recommendation
- Enforce role-based access control (RBAC) on the server side for all sensitive endpoints.
- Avoid relying on UI obscurity (e.g., hidden elements, CSS tricks) for access control.
- Log unauthorized access attempts and monitor endpoint access behavior.

---

### References
- [OWASP Access Control Cheat Sheet](https://cheatsheetseries.owasp.org/cheatsheets/Access_Control_Cheat_Sheet.html)
- [OWASP Top 10: A01:2021 – Broken Access Control](https://owasp.org/Top10/A01_2021-Broken_Access_Control/)
