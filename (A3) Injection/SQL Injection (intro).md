### Vulnerability Description  
The application does not properly validate or sanitize user input before constructing SQL queries. As a result, attackers can inject arbitrary SQL code into queries, allowing unauthorized data access, manipulation, and even destruction — violating the Confidentiality, Integrity, and Availability (CIA) triad.

---

### Steps Taken

1. **Introduced to SQL and CIA Goals**  
   The lesson begins with an overview of SQL, explaining DML, DDL, and DCL, and introduces SQL injection as a means to violate CIA principles.  
   ![a](https://github.com/user-attachments/assets/8a3cfa2e-4026-45c0-8f2d-b6a980b58aab)

2. **Viewed Sample Employee Table**  
   SQL query and table structure are explained using a realistic employee dataset.  
   ![b](https://github.com/user-attachments/assets/d494cdb4-5ffc-4b13-9bb3-0fbe04bf74a6)

3. **Targeted SELECT Query**  
   Tasked with retrieving Bob Franco's department without authentication.  
   ![c](https://github.com/user-attachments/assets/5a93b385-7782-420d-a6c0-fc1a1c9e3c79)

4. **Executed SELECT Query**  
   Used `SELECT department FROM employees WHERE first_name='Bob'` to retrieve data.  
   ![A3_2](https://github.com/user-attachments/assets/015e408d-a9dc-4b79-8137-dd2575c1a03e)

5. **DML Concepts and Examples**  
   Introduced SQL DML operations (SELECT, INSERT, UPDATE, DELETE) and their potential abuse.  
   ![d](https://github.com/user-attachments/assets/bbdee686-bc59-4cb9-b07b-1f57f5335878)

6. **Performed UPDATE Injection**  
   Updated Tobi Barnett’s department to ‘Sales’ using:  
   UPDATE employees SET department='Sales' WHERE first_name='Tobi'    
   ![e](https://github.com/user-attachments/assets/39ff6f57-d1e9-4249-bf4c-1354884c82c6)      
   ![A3_3](https://github.com/user-attachments/assets/38f19ef6-b605-420c-b8e9-8b0bb033a72c)  

7. **DDL Concepts and Injection Point**  
   Learned how DDL (CREATE, ALTER, DROP) statements can be abused.  
   ![f](https://github.com/user-attachments/assets/1caef001-4d01-4fca-9006-9ddbd39eb98d)

8. **Executed ALTER TABLE Query**  
   Added a new column using:  
   ALTER TABLE employees ADD phone varchar(20)  
   ![A3_4](https://github.com/user-attachments/assets/e7fab6ce-83d9-4ca1-ac9d-9a1977ef0a70)

---

10. **Severity and Exploitation Concepts**  
   Reviewed how attacker skill, lack of defense-in-depth, and backend language affect SQLi success.  
   ![lol](https://github.com/user-attachments/assets/6f3431cd-356b-4d9a-8abf-98bf60e02d95)  
   ![A3_5](https://github.com/user-attachments/assets/dcfab7da-a5fd-4667-92f0-0c6fe38a850d)

12. **What is SQL injection?**  
   Payloads like `' OR 1=1 --`, `' ; DROP TABLE users; --` are shown.  
    ![g](https://github.com/user-attachments/assets/a2639483-4c3f-4c56-9431-fa772c832bda)  
    ![h](https://github.com/user-attachments/assets/ce49332f-83ab-428a-b483-0491bd5c491d)  
    ![i](https://github.com/user-attachments/assets/40f1cea1-5260-4476-be29-db8104a194fe)

14. **Consequences of SQL injection**  
    ![j](https://github.com/user-attachments/assets/fea78560-e68f-4688-8c6d-35fea7002fb5)  

---

### Steps Taken

13. **Severity of SQL Injection**  
   The image outlines the severity of SQL injection attacks, explaining factors like the attacker's skill and the defense mechanisms that limit SQL injection's impact  
   ![k](https://github.com/user-attachments/assets/e395046d-ff70-4908-afc4-64a9b2428b81)

14. **Try It! String SQL Injection**  
   This screenshot shows an example of how SQL injection works in string-based queries, retrieving all users from the table by injecting a condition that always evaluates to true.
   ![l](https://github.com/user-attachments/assets/0ec5d45a-71e8-481f-b4ac-85da5bd2c19b)
   ![A3_6](https://github.com/user-attachments/assets/9d62abbf-09f7-4a36-9e2f-9726350f0608)

---

15. **Initial Confidentiality Challenge**  
   Input crafted as: `Smith' OR 1=1--` with valid TAN, resulting in unauthorized data exposure.  
   `![m](assets/m.png)`  
   `![A3_8](assets/A3_8.png)`

---

## A3 – CIA Violation: Integrity

### Vulnerability Description  
SQL query chaining allows unauthorized modification of sensitive values by injecting additional statements using `;`.

---

### Steps Taken
zzz
16. **Compromising Confidentiality with String SQL Injection**  
   A tutorial on compromising the confidentiality of data using string-based SQL injection. The user is asked to retrieve employee data without knowing specific names or TANs.
   ![lol2](https://github.com/user-attachments/assets/960f3fa7-a9ad-4449-9719-79b8fcdbc8e8)

17. **Increased Own Salary**  
   A demonstration of numeric SQL injection, where the user is tasked with retrieving all the data from the users' table by using SQL injection
   ![a3_9](https://github.com/user-attachments/assets/d459a2f4-b3fe-43db-bbe9-81048eb8c666)



### Steps Taken

18. **Compromising Confidentiality with String SQL Injection**  
    A tutorial on compromising the confidentiality of data using string-based SQL injection. The user is asked to retrieve employee data without knowing specific names or TANs. 
   ![0](https://github.com/user-attachments/assets/78d6590d-3a4b-4603-a03d-97425abe9c73)  
   ![a3_10](https://github.com/user-attachments/assets/2bc05dd9-789e-4ab2-94ec-e2bee0e50e39)

18. **Compromising Confidentiality with String SQL Injection**  
    A tutorial on compromising the confidentiality of data using string-based SQL injection. The user is asked to retrieve employee data without knowing specific names or TANs. 
   ![m](https://github.com/user-attachments/assets/1553ecb2-c207-427c-a175-7f3c83b92790)  
   ![a3_9](https://github.com/user-attachments/assets/c9122adb-36b2-45a8-8859-7fd2ace6fad7)

18. **Compromising Confidentiality with String SQL Injection**  
    A tutorial on compromising the confidentiality of data using string-based SQL injection. The user is asked to retrieve employee data without knowing specific names or TANs. 
   ![0](https://github.com/user-attachments/assets/78d6590d-3a4b-4603-a03d-97425abe9c73)  
   ![a3_10](https://github.com/user-attachments/assets/0b52c6d4-775e-4df2-91e0-608404f9d0ba)

<img width="965" alt="0" src="https://github.com/user-attachments/assets/2366adaa-facc-41a1-b37a-111da539ee9c" />

<img width="482" alt="a3_10" src="https://github.com/user-attachments/assets/0b52c6d4-775e-4df2-91e0-608404f9d0ba" />

### Risk Rating  
**Critical** – SQL Injection enables unauthorized read/write/delete operations on backend databases. It leads to full compromise of data confidentiality, tampering of integrity, and disruption of availability.

---

### Remediation Recommendations  
- Use **parameterized queries** (e.g., `PreparedStatement` in Java, PDO in PHP).  
- Enforce **strict input validation** with allow-lists.  
- Implement **least privilege** access for database users.  
- Sanitize all input using ORM frameworks or trusted libraries.  
- Log, monitor, and alert on suspicious SQL query patterns.  
- Apply security updates to database engines and libraries.

---

### References  
- [OWASP A03:2021 – Injection](https://owasp.org/Top10/A03_2021-Injection/)  
- [OWASP SQL Injection Prevention Cheat Sheet](https://cheatsheetseries.owasp.org/cheatsheets/SQL_Injection_Prevention_Cheat_Sheet.html)  
- [OWASP Testing Guide – SQL Injection](https://owasp.org/www-project-web-security-testing-guide/latest/4-Web_Application_Security_Testing/07-Input_Validation_Testing/04-Testing_for_SQL_Injection)  
- [CWE-89: Improper Neutralization of Special Elements in SQL Commands](https://cwe.mitre.org/data/definitions/89.html)
