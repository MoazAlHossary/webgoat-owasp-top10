# SQL Injection (advanced)

## Vulnerability Description

**Advanced SQL Injection** exploits occur when user input is unsanitized and inserted directly into SQL queries, especially when multiple techniques are chained.  
In this exercise, we were able to:
- Bypass authentication
- Dump user credentials
- Perform blind injections
- Use tools like Burp Intruder for automation

### 🔹 a
![a](https://github.com/user-attachments/assets/14039431-97fb-4f65-89ad-614b2798a8a9)  
Concept and goals

### 🔹 b
![b](https://github.com/user-attachments/assets/5c96178b-97af-4d6c-818b-a1cecbc741c0)  
The special characters and statements slide explains key syntax used in SQL injection. For example, -- is used for commenting out the rest of a query, and ' OR 1=1 -- is a classic bypass technique. It also highlights UNION for combining query results and JOIN for linking tables — both useful in advanced SQL injection scenarios.

### 🔹 c
![c](https://github.com/user-attachments/assets/352a2fa2-c468-49f3-b20b-217b17f33782)  
This slide introduces a hands-on challenge using two related tables: user_data and user_system_data. The user input is vulnerable, and by using UNION injection or appending new SQL statements, we are tasked with extracting user credentials such as Dave’s password. The schema structures help us craft accurate payloads.
### 🔹 A32_1
![A32_1](https://github.com/user-attachments/assets/52c6d3e0-965a-4d68-9329-65d07ad2dba5)  
6.a) Retrieve all data from the table
6.b) When you have figured it out…​. What is Dave’s password?

### 🔹 d
![d](https://github.com/user-attachments/assets/24c5d863-c38f-4cc3-922e-0bba84ba0a98)  
This is the concept overview for the lesson. It explains that the focus is on advanced SQL injection techniques such as combining multiple approaches and blind SQL injection, where responses are inferred from behavior instead of visible output.

### 🔹 e
![e](https://github.com/user-attachments/assets/a9a7e1ea-0d66-4d8a-a340-04455032a251)  
Goal: Can you log in as Tom?

### 🔹 A32_2
![A32_2](https://github.com/user-attachments/assets/d3372069-a0dc-4535-9f3c-1d4cae2b8cbc)  
The payload injects SQL logic through the registration form to identify if the first character of the password matches a guessed value.

### 🔹 A32_3
![A32_3](https://github.com/user-attachments/assets/6e33cedf-d4c0-46f7-9565-68f2a12da81e)  
Burp Suite Intruder is configured to brute force the correct characters using a payload list of lowercase letters.

### 🔹 a32_4
![a32_4](https://github.com/user-attachments/assets/8622df70-2b47-4d12-98bf-cd0ed2074031)  
payloads

### 🔹 A32_5
![A32_5](https://github.com/user-attachments/assets/7deb2436-13a3-40ef-a7a7-72830108da0c)  
The Intruder attack screen shows different response lengths, indicating successful character guesses via response difference.

### 🔹 a32_6
![a32_6](https://github.com/user-attachments/assets/32ac3500-f677-42aa-acae-58abdc313798)  
A Python script automates the attack by checking each character using substring comparison and analyzing server feedback.

### 🔹 a32_7
![a32_7](https://github.com/user-attachments/assets/28e65a18-b47f-4092-915a-87d3ea473d47)  
The script prints the successfully recovered password based on the feedback content returned from the server.

### 🔹 a32_8
![a32_8](https://github.com/user-attachments/assets/9fce98ef-b8a6-474f-8bfb-b4347d2af00a)  
After retrieving the password, logging in as Tom confirms that the full account access was successfully achieved.

### 🔹 a32_9
![a32_9](https://github.com/user-attachments/assets/b43d28ad-bdb8-406d-a569-5cb24cbaea51)  
Quiz



## Recommmended Remediation

To mitigate advanced SQL Injection:
- ✅ Use **parameterized queries** and stored procedures
- ✅ Avoid direct user input in dynamic SQL commands
- ✅ Utilize WAFs and runtime protection tools
- ✅ Limit database permissions based on the principle of least privilege
- ✅ Sanitize input using both client and server-side validation
- ✅ Regularly test your apps with automated tools and **manual code reviews**

---

## 🔗 References
- [OWASP Advanced SQLi](https://owasp.org/www-community/attacks/SQL_Injection)
- [SQLi Prevention Cheat Sheet](https://cheatsheetseries.owasp.org/cheatsheets/SQL_Injection_Prevention_Cheat_Sheet.html)
- [WebGoat GitHub](https://github.com/WebGoat/WebGoat)
"""

