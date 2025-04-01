# OWASP A3: Injection – SQL Injection (Advanced)

## Vulnerability Description

SQL injection remains one of the most dangerous web vulnerabilities due to its ability to affect confidentiality, integrity, and availability of backend systems. While input filtering can provide a first layer of defense, it is easily bypassed. The only reliable defense is to use **parameterized queries**, **stored procedures**, and to apply **input validation**.

---

## Screenshots

### 🔹 `1.png`  
![1](https://github.com/user-attachments/assets/d8ada267-3587-4390-ba9d-29dfceca8594)  
**Immutable Queries** — Demonstrates how static queries and properly parameterized queries are resistant to injection.

### 🔹 `2.png`  
![2](https://github.com/user-attachments/assets/86c5ad30-0777-4e93-9037-fdcad8fe9974)  
**Stored Procedures** — Shows safe vs. unsafe stored procedures. Safe ones use parameters; unsafe ones concatenate SQL dynamically.

### 🔹 `3.png`  
![3](https://github.com/user-attachments/assets/314c061b-3ac4-437b-94fd-ab64faf6e094)  
**Parameterized Queries – Java Snippet** — Example of safe SQL usage with `PreparedStatement` and `setString()` in Java.

### 🔹 `4.png`  
![4](https://github.com/user-attachments/assets/14a4f14c-6a6d-46cb-8dbf-a21c1a1e351a)  
**Parameterized Queries – Java Example** — Demonstrates secure query execution using `PreparedStatement` and result processing.

### 🔹 `5.png`  
![5](https://github.com/user-attachments/assets/8ddd24c3-8506-4c1a-872c-82ab75a65002)  
**Try It – Writing Safe Code** — Writing safe JDBC to retrieve user status using both `name` and `email` with bound variables.

![a32_10](https://github.com/user-attachments/assets/6e74b386-b632-4c9f-a20b-84d91f9d2569)  
**Success Message** — Confirmed secure implementation.

### 🔹 `6.png`  
![6](https://github.com/user-attachments/assets/61c9d6f6-ac7d-489b-b4ca-1b4e6c80f014)  
**Try It – Writing Safe Code (From Scratch)** — Build Java code using JDBC and prepared statements to safely fetch user data.

![a32_11](https://github.com/user-attachments/assets/23113e34-118c-4182-9cd6-c2ae743e418d)  
**Success** — Code passes the test for SQLi protection.

### 🔹 `7.png`  
![7](https://github.com/user-attachments/assets/50f18fa9-cbd2-4d1b-bfb2-8d5e985e45d8)  
**Parameterized Queries – .NET** — Example of using `.Add()` to safely pass input to SQL queries via `SqlCommand` in .NET.

### 🔹 `8.png`  
![8](https://github.com/user-attachments/assets/497aea0b-2ecb-4cf6-9d55-6334bab9c361)  
**Input Validation Required?** — Clarifies why filtering alone is not sufficient, and input validation is still necessary even with prepared statements.

---

## Observed Behavior

- Unsafe input concatenation remains vulnerable despite basic filters (e.g., stripping spaces).
- Even non-dynamic parts like `ORDER BY` clauses can be exploited if not explicitly validated.
- Secure use of `PreparedStatement` and regex-based input validation in Java/.NET effectively blocks SQLi.

---

## Remediation

- Always use **prepared statements** instead of building SQL strings dynamically.
- Validate inputs **before** passing them to queries, using **whitelisting** patterns.
- Protect `ORDER BY`, `LIMIT`, or other expressions that cannot use bind variables.
- Use **least privilege** when connecting to the database.
- Employ stored procedures **without dynamic SQL** wherever possible.

---

## References

- [OWASP SQL Injection Prevention Cheat Sheet](https://cheatsheetseries.owasp.org/cheatsheets/SQL_Injection_Prevention_Cheat_Sheet.html)
- [OWASP Java Encoder Project](https://owasp.org/www-project-java-encoder/)
- [OWASP .NET Security Cheat Sheet](https://cheatsheetseries.owasp.org/cheatsheets/ASPNET_Security_Cheat_Sheet.html)
- [OWASP Input Validation Cheat Sheet](https://cheatsheetseries.owasp.org/cheatsheets/Input_Validation_Cheat_Sheet.html)
