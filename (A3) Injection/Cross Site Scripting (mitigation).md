A3: Cross Site Scripting (Mitigation)

##  Vulnerability Description
Cross-Site Scripting (XSS) mitigation involves implementing security measures to prevent attackers from injecting malicious scripts into web applications. This lesson focuses on both stored and reflected XSS, as well as the best practices and encoding methods that help protect against these vulnerabilities. It emphasizes the importance of context-aware encoding, proper data sanitization using tools like OWASP’s AntiSamy, and understanding how data is rendered in client-side code.

---

## Steps

###  Concept and Goals
![a.png](https://github.com/user-attachments/assets/35020e56-02e4-4f54-88e0-fcbddb8e637f)

###  XSS Defense Overview
To defend against XSS, always encode untrusted user input before sending it to the browser, based on where it is placed (HTML body, attribute, or JavaScript). This ensures that input is treated as data, not executable code. Never rely on blacklists—use proper output encoding instead.
![b.png](https://github.com/user-attachments/assets/891e2e9e-3462-4b30-9d89-9f47538c0981)

###  What is Encoding and Escaping
Encoding converts special characters (like <, >, &, ') into safe representations (like &lt;, &gt;) to prevent them from being executed as code. Escaping user input like this helps protect against XSS by ensuring input is displayed as plain text, not HTML or JavaScript.
![c.png](https://github.com/user-attachments/assets/b6f0ea16-b804-46f1-ad46-c92569cf0f4a)

###  XSS Defense Resources
This image provides links and tools (like OWASP Java Encoder, XSS cheat sheets, and JavaScript framework guidance) to help developers prevent XSS by properly encoding user input and avoiding unsafe coding practices.
![d.png](https://github.com/user-attachments/assets/6f85cff1-1977-4b88-9c66-5dd79c413f25)

###  Reflective XSS – Unescaped Input in JSP
The JSP file outputs user input (first_name, last_name) without escaping, allowing JavaScript to be injected and executed in the browser. This creates a reflected XSS vulnerability and must be fixed using output encoding like e:forHtml().
![e.png](https://github.com/user-attachments/assets/d014dc0e-b38e-4933-8bf8-173c9ff096dc)

###  Reflective XSS – Your Turn to Escape Parameters
The task is to fix a reflected XSS issue by escaping user input in the JSP file. You must replace the unescaped request.getParameter() calls with a secure method like e:forHtml() to prevent injected scripts from executing.
![f.png](https://github.com/user-attachments/assets/f33e8765-fdce-45f5-acfd-32061abaaf19)

###  Escaping User Input in JSP with OWASP Java Encoder
This solution shows the correct way to prevent XSS by escaping user input using the e:forHtml() method from the OWASP Java Encoder. It ensures that any potentially dangerous characters (like < or >) are safely rendered as plain text in the browser.
![g.png](https://github.com/user-attachments/assets/f139b0a4-c7cd-438e-8de6-234d6821308d)

###  Unsafe Stored Input in Java (Stored XSS Risk)
This example shows a stored XSS vulnerability caused by saving raw user input to the database without sanitization. The data is inserted using PreparedStatement, but without cleaning it, malicious scripts can be stored and later executed when rendered.
![h.png](https://github.com/user-attachments/assets/424e0764-0f71-4ed8-9c8c-544c46ba40f2)

###  Fixing Stored XSS with AntiSamy (Your Turn)
This task requires using OWASP AntiSamy to sanitize the comment before saving. It prevents malicious input from being stored by cleaning the HTML using a predefined policy (antisamy-slashdot.xml).
![i.png](https://github.com/user-attachments/assets/ac08215f-cf7c-484c-be4d-377ef91ae31d)

###  Completed: Clean Input Stored with AntiSamy
![j.png](https://github.com/user-attachments/assets/f41f978b-c383-4a89-bbf9-1080adec1193)

---

##  Observed Behavior
In the lesson walkthrough, the application shows how vulnerable JSP code prints user inputs directly without encoding them, which makes it susceptible to XSS. You then learn how to mitigate this by:

- Escaping HTML output in JSP using `e:forHtml`
- Using AntiSamy to sanitize inputs before storing them in the database
- Understanding encoding needs depending on context (HTML body, JavaScript, attributes, etc.)

---

## Recommended Remediation

To prevent Cross-Site Scripting attacks:
- Always encode user input based on output context (HTML body, attribute, JavaScript, URL, etc.).
- For Java applications, use libraries like [OWASP Java Encoder](https://owasp.org/www-project-java-encoder/) and [AntiSamy](https://owasp.org/www-project-antisamy/) for safe output.
- Do not blacklist characters manually; instead, use whitelisting and output encoding.
- In JSPs, use `${e:forHtml(param.xyz)}` to properly escape variables.
- Avoid rendering raw user input without sanitization or escaping.

---
  
##  References
- [OWASP XSS Prevention Cheat Sheet](https://cheatsheetseries.owasp.org/cheatsheets/Cross_Site_Scripting_Prevention_Cheat_Sheet.html)
- [DOM XSS Prevention Cheat Sheet](https://cheatsheetseries.owasp.org/cheatsheets/DOM_based_XSS_Prevention_Cheat_Sheet.html)
- [OWASP AntiSamy](https://owasp.org/www-project-antisamy/)
- [OWASP Java Encoder](https://owasp.org/www-project-java-encoder/)
"""
