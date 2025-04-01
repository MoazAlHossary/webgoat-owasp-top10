
# A5: Cross-Site Request Forgery (CSRF)

**Vulnerability Description:**  
CSRF (Cross-Site Request Forgery) allows an attacker to trick a user’s browser into sending unintended requests to a web application where the user is authenticated. These forged requests inherit the user's session and permissions, allowing unauthorized actions to be performed on the user's behalf.

---

## A. CSRF Module Overview  
![A](https://github.com/user-attachments/assets/d94b83c3-65ed-46f1-b327-ee8c2d4122bd)  
Introductory page explaining how CSRF exploits trusted user sessions via cross-origin requests.

## B. Task Instructions  
![B](https://github.com/user-attachments/assets/d28d555a-ab36-49d5-81ff-0f452e5edd50)  
Setup for a basic CSRF GET challenge that requires an authenticated user.

## C. Exercise Objective  
![C](https://github.com/user-attachments/assets/163df7fb-3b5c-4c9f-8e68-ce5c53fbcd32)  
Demonstrates CSRF success by submitting a flag using a forged request.

## D. Capturing Target Request  
![D](https://github.com/user-attachments/assets/ccfbcc66-90a4-48b9-8bc1-3cddb67a2730)  
Shows how to intercept the CSRF POST request using Burp Suite.

## E. CSRF Exploit HTML Form  
![E](https://github.com/user-attachments/assets/01f52b78-cc42-4ebb-b01b-a38adfa5e394)  
An attacker’s HTML form crafted to send a POST request imitating a user.

## F. CSRF Payload Execution  
![F](https://github.com/user-attachments/assets/048a041a-2aa8-43dd-8dd1-2802e94cd243)  
The malicious HTML file opened locally to simulate an actual CSRF attack.

## G. Successful CSRF Execution  
![G](https://github.com/user-attachments/assets/dd956859-7dd5-428d-8d72-71983513d724)  
Server returns a valid flag after a successful forged request.

## H. Flag Confirmation  
![H](https://github.com/user-attachments/assets/9c6fe8fb-1e4b-4566-84e1-d16eda1c19ea)  
Flag submission confirms successful GET CSRF.

## I. Review Submission Challenge  
![I](https://github.com/user-attachments/assets/e229fa26-9ac4-4970-ba0a-2ba3d1660a41)  
Task: perform CSRF to submit a fake review as a logged-in user.

## J. Same-Origin Enforcement  
![J](https://github.com/user-attachments/assets/95395b6d-d4d9-4ef1-82ee-07689b7709f2)  
CSRF request was blocked due to same-origin delivery.

## K. Crafted HTML Review Form  
![K](https://github.com/user-attachments/assets/d853d83e-970b-41f6-bf45-c2afaa11673d)  
HTML form built to simulate a legitimate review submission.

## L. Hosting the CSRF Form Locally  
![L](https://github.com/user-attachments/assets/3d0798c5-d181-4aed-9994-b6e2177968fc)  
HTML file hosted and run locally to test CSRF.

## M. Review Posted via CSRF  
![M](https://github.com/user-attachments/assets/7f2f310d-7435-4f7b-b1da-dc9c1f7e2f2a)  
Fake review appears, showing that CSRF succeeded.

## N. JSON-Based CSRF Challenge  
![N](https://github.com/user-attachments/assets/b0e46281-6f6a-42b7-8e1b-1462492bd1d4)  
Challenge to submit a JSON payload using a CSRF POST.

## O. JSON Payload Format  
![O](https://github.com/user-attachments/assets/c2fbcf69-5acb-4e9e-8465-fb3f2b5d1d3a)  
Example format of the required JSON body.

## P. Attempted Fetch Attack  
![P](https://github.com/user-attachments/assets/67454848-c2a3-4a15-8637-ce343c1e21e2)  
Script attempts to use `fetch()` with JSON from another origin.

## Q. CORS Policy Blocks Request  
![Q](https://github.com/user-attachments/assets/06f7a301-fb89-4b15-9dcc-1ba53056ae38)  
CORS restrictions prevent fetch-based CSRF from succeeding.

## R. HTML Form with `enctype=text/plain`  
![R](https://github.com/user-attachments/assets/37e872a5-08a8-4f8c-adfa-27cb613b8cf9)  
HTML form used to bypass content-type restrictions using `text/plain`.

## S. CSRF Form Submitted  
![S](https://github.com/user-attachments/assets/b4b55036-c0ec-4750-88f6-87fd150c2acc)  
The server accepted the forged request from a valid-looking form.

## T. Server Returns Valid Flag  
![T](https://github.com/user-attachments/assets/f7404521-7681-470e-92f7-03728c203906)  
The challenge returns a flag, confirming the CSRF worked.

## U. Final Confirmation  
![U](https://github.com/user-attachments/assets/49c7161e-a877-4c2e-bc11-663a61e15674)  
Module acknowledges completion of the CSRF challenge.

## V. Login CSRF Attack Overview  
![V](https://github.com/user-attachments/assets/d7be950d-640d-4a60-aa24-c0e17b5c1809)  
Illustrates how an attacker forces a victim to log in with attacker’s credentials.

## W. Logged in as `csrf-tom`  
![W](https://github.com/user-attachments/assets/9e929606-a080-41d5-841d-d6ae732330a9)  
Victim ends up logged in as the attacker's controlled user.

## X. WebGoat Flags Login CSRF as Completed  
![X](https://github.com/user-attachments/assets/c5c3ca23-61b6-44da-a956-102b7419f348)  
Final confirmation that the login CSRF exploit worked.

---

## Observed Behavior
- Multiple actions could be triggered from another domain while authenticated.
- CSRF attacks succeeded with both GET and POST methods.
- Login CSRF was demonstrated, showing session hijack.

## Remediation

- Use **CSRF tokens** on all state-changing requests.
- Set cookies to **SameSite=Strict** or **Lax**.
- Validate **Referer** and **Origin** headers server-side.
- Require **user re-confirmation** for critical changes.
- Accept only known **Content-Type** values.

## References
- [OWASP CSRF Overview](https://owasp.org/www-community/attacks/csrf)  
- [CSRF Prevention Cheat Sheet](https://cheatsheetseries.owasp.org/cheatsheets/Cross-Site_Request_Forgery_Prevention_Cheat_Sheet.html)  
- [MDN Web Docs - CSRF](https://developer.mozilla.org/en-US/docs/Glossary/CSRF)  
