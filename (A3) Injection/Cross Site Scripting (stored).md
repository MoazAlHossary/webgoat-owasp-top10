# Cross Site Scripting (stored)

## Vulnerability Description

**Stored Cross-Site Scripting (Stored XSS)** occurs when malicious input provided by an attacker is stored persistently on the target server, such as in a database, message forum, visitor log, comment field, etc., and later rendered to users without proper sanitization. Unlike reflected XSS, which requires a user to click a malicious link, stored XSS automatically executes when the victim loads the infected page. This makes it more dangerous and effective for targeting multiple users.


### 🔹 concept and goals  
![a.png](https://github.com/user-attachments/assets/6b373da5-cdbb-444e-a8ef-d3a2e38ab008)  

---

### 🔹 stored xss scenario  
![b.png](https://github.com/user-attachments/assets/b33e181c-c434-4899-9c45-da925dbb3870)  
This diagram explains the **stored XSS attack flow**. The attacker posts a malicious script on a message board, which is stored in the server database and executed when another user reads it. The user does not realize they’ve been attacked.

---

### 🔹javascript payload  
![c.png](https://github.com/user-attachments/assets/dc532aa4-2dfb-40d0-b7aa-fcc5b695e973)  

Add a comment with a JavaScript payload. Again … you want to call the webgoat.customjs.phoneHome function.

As an attacker (offensive security), keep in mind that most apps will not have such a straightforwardly named compromise. Also, you may have to find a way to load your JavaScript dynamically to achieve the goal of extracting data fully.

---

### 🔹 phonehome triggered  
![d.png](https://github.com/user-attachments/assets/f8f1847e-4fcc-4d76-b42b-484ff3cf3930)  
A demonstration of submitting a malicious comment using `<script>webgoat.customjs.phoneHome()</script>`, which is the expected payload to simulate stored XSS.


---

### 🔹 comments list (injection field)  
![e.png](https://github.com/user-attachments/assets/6a6c81c8-491e-4af3-a399-21a54cbe31e6)  
This output in the developer console confirms that the XSS payload was executed and the `phoneHome` method was invoked, providing a random response number indicating successful exploitation.

---


## Observed Behabior
- The application allowed user-submitted comments to be stored and rendered without proper sanitization.
- A malicious JavaScript payload (<script>webgoat.customjs.phoneHome()</script>) was injected into a comment field.
- Upon revisiting the page containing the stored comment, the script executed automatically in the context of the victim's browser.
- The developer console showed confirmation that the phoneHome function was triggered, indicating successful script execution.
- No input validation, escaping, or content filtering was observed at the point of storage or rendering, allowing persistent script execution for all users viewing the affected page.

## Recommended Remediation

- Sanitize and encode all user input before rendering it in the browser.
- Use frameworks or templating engines that automatically escape XSS by design.
- Apply Content Security Policy (CSP) to reduce the chances of executing injected scripts.
- Implement proper output encoding especially for data shown in HTML, JavaScript, or attributes.

---

## References

- [OWASP XSS Prevention Cheat Sheet](https://cheatsheetseries.owasp.org/cheatsheets/Cross_Site_Scripting_Prevention_Cheat_Sheet.html)
- [OWASP DOM based XSS Prevention](https://cheatsheetseries.owasp.org/cheatsheets/DOM_based_XSS_Prevention_Cheat_Sheet.html)
- [PortSwigger: Stored XSS](https://portswigger.net/web-security/cross-site-scripting/stored)
