# OWASP A7: Cross Site Scripting (XSS)

## Vulnerability Description

Cross-Site Scripting (XSS) is a client-side vulnerability that allows an attacker to inject malicious scripts into webpages viewed by other users. These scripts can hijack sessions, redirect users, steal credentials, and manipulate webpage content. Common types include Reflected XSS, Stored XSS, and DOM-Based XSS.


## Screenshots (Alphabetical Order)

###  concept and goals
Concept and goals of the XSS lesson in WebGoat, outlining learning objectives including reflected and DOM-based XSS
![a.png](https://github.com/user-attachments/assets/da2768a3-671e-4ff9-84ed-4e1e166b4432)

###  what is xss?
Explanation of what Cross-Site Scripting (XSS) is, including its definition and potential impacts on web application security
![b.png](https://github.com/user-attachments/assets/57b9a2e6-b1e5-442b-9821-859d0244a966)

###  most common locations
List of common locations where XSS vulnerabilities are found, such as input fields and search bars that reflect user input.
![c.png](https://github.com/user-attachments/assets/f2e9fb76-e123-4805-8bd1-0372cec1dda0)

###  why should we care
Highlights the reasons why XSS is a significant threat, including stealing session cookies and executing malicious code.
![d.png](https://github.com/user-attachments/assets/e2608bf8-5fa6-4ef8-8616-d00961ad7859)

###  types of xss
Overview of XSS types with emphasis on the importance of domain trust and how attackers manipulate trust for phishing
![e.png](https://github.com/user-attachments/assets/ca1c7b0d-113b-4e44-a545-a841ac840c9b)

###  reflected xss scenario
Diagram and explanation of a reflected XSS attack flow, showing the attacker, victim, and the application's response.
![f.png](https://github.com/user-attachments/assets/64274458-0d80-48a6-8b4f-5b2b9c2164ee)

###  try it reflected xss
A WebGoat interactive lesson instructing users to find a field vulnerable to reflected XSS in a shopping cart form.
![g.png](https://github.com/user-attachments/assets/b7aafd5e-1853-49f2-b337-8036eb1b5166)

###  self xss or reflected xss
Clarification of the difference between self-XSS and reflected XSS by showing a test URL used in the WebGoat lab.
![j.png](https://github.com/user-attachments/assets/9e62a6a9-0099-400d-b1db-8ebc56efac16)

###  reflected or dom based xss
Explanation of reflected and DOM-based XSS, noting that DOM XSS occurs entirely in the client-side browser context.
![k.png](https://github.com/user-attachments/assets/daf16cee-0cee-4a6d-945f-3b9d652ea43b)

###  identify potential for dom based xss
Prompt from WebGoat asking users to identify the route that handles input in a way that could lead to DOM-based XSS
![l.png](https://github.com/user-attachments/assets/cb7c231a-5612-4f43-a676-fd444942d888)

###  try it dom based xss
Initial 'Try It!' section for DOM-Based XSS, asking the user to call a JS function via a vulnerable route to complete the lab.
![m.png](https://github.com/user-attachments/assets/cc63c4e2-611b-4385-bfb4-dc136625f5ec)

###  try it reflected xss
Execution of a reflected XSS payload inside a form field, confirming which field is injectable using `alert()`."
![n.png](https://github.com/user-attachments/assets/a02d1bc1-9270-40c3-9c31-9c8654bc6ee5)

###  success
Completion of the XSS reflected payload execution, with the alert removed but injection confirmed in the DOM."
![o.png](https://github.com/user-attachments/assets/f4059976-d905-45c8-b157-beb9d80cec04)

###  hint
Hint panel advising users to inspect the client-side code using browser developer tools to locate vulnerable JavaScript.
![p.png](https://github.com/user-attachments/assets/dce86b4e-2526-44fa-8a21-ff9820aa8e0c)

###  dev tools source code
the browser dev tools showing goatApp.js code for route definitions, useful in identifying DOM XSS.
![q.png](https://github.com/user-attachments/assets/1b17fc00-60df-459b-b2c0-1ea433abbbde)

###  test/parm
JavaScript route definitions from goatApp.js showing the `/test/:param` route which is vulnerable to DOM XSS.
![r.png](https://github.com/user-attachments/assets/503a7a3f-e623-4552-901a-3fbe266c40e3)

###  sucess
Successful submission of the `/test/` route payload in DOM-based XSS to complete the challenge.
![s.png](https://github.com/user-attachments/assets/5c173e47-0483-4375-8b66-2dde33f69aa8)

###  go to linke found
URL input that includes a script payload targeting `webgoat.customjs.phoneHome()` function execution for DOM XSS.
![t.png](https://github.com/user-attachments/assets/4cfde41a-3086-40e5-a671-a773d675a705)

###  f12
Final submission screen showing `phoneHome()` triggered, returning a unique number for DOM XSS completion.
![u.png](https://github.com/user-attachments/assets/ba8c2812-814d-48ce-9ec3-7decb5e0e68e)

###  success
Successful completion of the WebGoat DOM XSS challenge verified by the returned unique number in console output
![v.png](https://github.com/user-attachments/assets/2685e8c9-1d46-4497-a659-71569aa0f31d)    




![z.png](https://github.com/user-attachments/assets/f7da907b-43af-42ac-ad54-35605e4865a3)


## Observed Behavior

- XSS payloads like `<script>alert(document.cookie)</script>` executed in forms and parameters.
- DOM-based attacks exploiting URL fragments to trigger client-side JavaScript.
- Reflected input in error messages or HTTP headers rendered without sanitization.
- Exploitation through credit card fields in the WebGoat shopping cart demo.
- Successful DOM-based XSS with endpoint `start.mvc#test/`.


## Recommended Remediation

- Always **escape output** especially when injecting into HTML, JS, or URLs.
- Use secure frameworks that **automatically encode output**.
- Validate all input on **both client and server sides**.
- Employ **Content Security Policy (CSP)** to restrict script execution.
- Sanitize HTML with libraries like DOMPurify for rich text input.

## References

- [OWASP XSS Prevention Cheat Sheet](https://cheatsheetseries.owasp.org/cheatsheets/XSS_Prevention_Cheat_Sheet.html)
- [OWASP DOM-Based XSS Wiki](https://owasp.org/www-community/attacks/DOM_Based_XSS)
- [OWASP Cross Site Scripting Explained](https://owasp.org/www-community/attacks/xss/)
