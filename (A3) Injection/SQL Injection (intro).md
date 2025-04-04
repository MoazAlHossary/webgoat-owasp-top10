# SQL Injection (intro)


This module explores how poorly sanitized user input can be leveraged to perform SQL injection attacks, manipulate backend databases, and violate application security. Below are key slides, exercises, and completed tasks from the WebGoat A3 SQL Injection module.


---

###  **Concept and Goals**   
  ![a](https://github.com/user-attachments/assets/36b3a212-7d73-4979-9c5d-6c55941ee88b)  
 
 Introduces the scope of SQL injection and how it can compromise the Confidentiality, Integrity, and Availability (CIA) triad.  

### **What is SQL?**  
  ![b](https://github.com/user-attachments/assets/2be859b5-e314-477d-98a5-4eebbb522966)    
 Shows how SQL is structured to store, retrieve, and modify data—making it a target for injection attacks.  

### **Retrieve department of Bob**
  ![c](https://github.com/user-attachments/assets/dcac0c45-734c-4913-af04-aadf3b9c484e)    
 Demonstrates use of a SELECT statement to pull specific user data.    
  ![A3_2](https://github.com/user-attachments/assets/433da1a6-6249-41ff-8281-8e09d58387b5)  
 Simple query shows how direct access to employee data can violate privacy.  

### **DML - Data Manipulation Language**   
  ![d](https://github.com/user-attachments/assets/b216dc97-6eb3-46d9-bfda-a4623e8d2be3)  
 DML commands like UPDATE and DELETE are used to alter or remove existing records.  

### **Change department to Sales**   
  ![e](https://github.com/user-attachments/assets/92b7a26d-7519-4eb7-a361-2c23f5524aa0)   
 Shows how the UPDATE command can be injected to change user roles.    
  ![A3_3](https://github.com/user-attachments/assets/298999d1-dbd5-4e25-93c3-d31320ac7b01)

### **DDL - Alter Table Schema**   
  ![f](https://github.com/user-attachments/assets/265a00f4-b564-42a5-a75f-2bb5ea2d8b47)   
 SQL injection used to add a column to the database schema.    
  ![A3_4](https://github.com/user-attachments/assets/a7e6434e-a9f3-4193-81dc-0653ed6fc927)

### **Grant privileges using DCL**  
  ![lol](https://github.com/user-attachments/assets/d6812229-17b0-491f-bb52-fb0a4d0a5480)  
 SQL injection used to escalate privileges via GRANT command.    
  ![A3_5](https://github.com/user-attachments/assets/7f8f414f-4700-41f5-b291-82cb45a0c0a8)

### **What is SQL Injection?**   
  ![g](https://github.com/user-attachments/assets/457c9177-137d-43c2-ae80-7fae79838b5b)   
 Highlights the danger of passing user input directly into SQL queries.  

### **Example Query Injection**
  ![h](https://github.com/user-attachments/assets/a77fd4c2-91ce-47b2-b4c9-2938d9a04e07)    
 Demonstrates unsafe query building using string concatenation.  
 
### **Classic Examples**   
  ![i](https://github.com/user-attachments/assets/87fc9ede-3c98-46dd-bf83-16d55200f3dd)  
 Shows common payloads like `' OR 1=1 --` to bypass login.  

### **Consequences**   
  ![j](https://github.com/user-attachments/assets/eca972d7-09e1-45b2-9910-daeebfea2f89)  
 SQLi can lead to data theft, manipulation, system control, or even OS commands.  

### **Severity of SQLi**   
  ![k](https://github.com/user-attachments/assets/771fd5ce-bf4a-4b5d-a473-0afbec92f549)  
 Explains how some platforms and mitigations reduce or prevent chaining and injection.

### **Try It! String Injection**   
  ![l](https://github.com/user-attachments/assets/9088f3b1-da60-417f-bd76-925abb0d6279)   
 Injected payload returns entire users table due to `OR '1'='1'`.    
  ![A3_6](https://github.com/user-attachments/assets/a06b756d-ec75-4db6-b832-8f402995456c)

### **Exfiltrated salaries**   
  ![lol2](https://github.com/user-attachments/assets/8efb6216-2a9d-40c1-9123-3fc587898186)   

  ![A3_7](https://github.com/user-attachments/assets/228d18d7-b467-4fc4-8e85-776521e93443)  
 SQLi used to bypass TAN check and dump internal salary info.  

### **Confidentiality Breach**  
  ![m](https://github.com/user-attachments/assets/dddd291c-f4c1-457a-8339-099ab5f9d9ad)  
 Used injection to view protected internal employee data.    
  ![A3_8](https://github.com/user-attachments/assets/59d34e17-0672-4807-a953-1992d272a5fc)

### **String Injection — Dump All**  
  ![lol3](https://github.com/user-attachments/assets/ec20b5be-b434-4b42-9aa4-528df9e20ede)  
 Query logic manipulated to always return `TRUE`.    
  ![a3_9](https://github.com/user-attachments/assets/365f206d-16c4-45ee-9ee2-a8a89fd1ffea)

### **Compromising Availability**  
  ![0](https://github.com/user-attachments/assets/38bcdbf2-827b-48a3-a25d-186752b7a58c)    
 SQL injection used to DROP the access_log table and erase tracks.    
  ![a3_10](https://github.com/user-attachments/assets/63e4c418-96cb-44e6-ac2e-c4f2fd4cfa73)


## Vulnerability Description

**SQL Injection (SQLi)** occurs when unsanitized user inputs are directly included in SQL queries, allowing attackers to manipulate the logic of those queries. This opens the door to unauthorized data access, modification, or deletion. In severe cases, an attacker can execute administrative operations or operating system commands via the database engine.

In WebGoat, several forms of SQLi were demonstrated:
- **String SQL Injection**: injecting `OR '1'='1` into fields using string concatenation.
- **Numeric SQL Injection**: modifying logic using numbers (e.g., `1 OR 1=1`).
- **Query Chaining**: using `;` to append additional statements.
- **DML/DDL/DCL Exploitation**: modifying or revoking user privileges and altering schema/data.

---

## Observed Behavior

During these exercises, it was possible to:
- Retrieve all user records without proper authentication
- Change salary and department fields to gain unauthorized benefits
- Drop or alter database schema and tables
- Delete logs to eliminate traces of tampering
- Escalate access control via `GRANT` commands
- Fully bypass input filters by exploiting SQL concatenation in backend queries

All actions were possible through form fields and GET/POST parameters without any rate-limiting, WAF, or prepared statements.

---

## Recommended Remediation

To prevent SQL injection:
- Use **parameterized queries** (prepared statements)
- Never directly concatenate user inputs into SQL queries
- Validate inputs using **whitelisting** techniques (never blacklist alone)
- Restrict DB permissions (least privilege principle)
- Disable stacked queries if not needed
- Employ **Web Application Firewalls (WAFs)** and continuous monitoring
- Regularly test applications via automated and manual **security scans**

---

## References

- [OWASP SQL Injection](https://owasp.org/www-community/attacks/SQL_Injection)
- [SQLi Prevention Cheat Sheet](https://cheatsheetseries.owasp.org/cheatsheets/SQL_Injection_Prevention_Cheat_Sheet.html)
- [OWASP Top 10 Project](https://owasp.org/www-project-top-ten/)
- [SQLCourse.com](http://www.sqlcourse.com/)
