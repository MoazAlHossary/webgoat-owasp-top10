# OWASP WebGoat - A4: XML External Entities (XXE)


## Vulnerability Description
**XML External Entity (XXE)** is a vulnerability that allows an attacker to interfere with an application’s XML processing. It can lead to data exposure, internal file disclosure, server-side request forgery, or even code execution. The root cause is the insecure configuration of XML parsers which allow external entities to be defined and resolved.
  
This lesson introduces XML External Entity (XXE) vulnerabilities, their abuse, and protection mechanisms. The goals are to understand XML structure, XML parser behavior, and how to exploit XXE.

![a](https://github.com/user-attachments/assets/3955d090-7c7d-4ed7-82b3-3b9fe7b11056)

---

##  XML Entity Basics
Demonstrates how XML parsers resolve internal entities by replacing them with defined values, laying the groundwork for XXE exploitation.
![b](https://github.com/user-attachments/assets/960f2cf2-430c-4722-a69b-db77b5ba33ff)  

Explains how XML input is parsed and shows how XXE vulnerabilities arise when external entities are processed, potentially allowing attackers to exfiltrate sensitive files or conduct internal network scans.
![c](https://github.com/user-attachments/assets/db50eaae-a635-413a-ab9b-917d08c88a9c)

---

##  External DTD Inclusion Example
Demonstrates how external DTDs and XML entities can be abused to perform XXE attacks, including accessing local files like /etc/passwd by referencing them through the SYSTEM identifier inside a crafted XML payload
![d](https://github.com/user-attachments/assets/8c3f9157-e715-44f6-8741-f5cbfcaa66ab)  

Shows a successful XXE attack where an XML parser loads the contents of /etc/passwd using an external entity. The file content is injected into the XML response, illustrating how a vulnerable parser can leak local files.
![e](https://github.com/user-attachments/assets/0be74acc-6295-4a83-9132-824047e0e67e)

---


##  Successful XXE Exploit
This image introduces a practical assignment in which the user is prompted to exploit an XXE vulnerability by injecting a malicious payload into the comment field of a photo post, targeting file system disclosure
![h](https://github.com/user-attachments/assets/f9792013-ee32-4b60-87c5-7f658bfb6700)

---

##  Exploit Payload
 This image shows an initial attempt to exploit the XXE vulnerability by submitting a crafted XML payload through Burp Suite. However, the response indicates failure (lessonCompleted: false) and a feedback message saying the solution is not correct, meaning the payload did not successfully trigger the vulnerability.
![i](https://github.com/user-attachments/assets/5051ef4c-aaca-4bfb-be05-f440ed1a4f2a)

---

##  Flag Submission
This image shows the successful execution of an XXE attack using Burp Suite. A malicious XML payload was sent containing a DOCTYPE definition with an external entity referencing a file (e.g., /). The server responded with a success message (lessonCompleted: true) and confirmed completion of the XXE assignment, indicating the vulnerability was exploited correctly.
![j](https://github.com/user-attachments/assets/2569e62c-305b-4463-a0f1-cb6cbb28810b)

---

##  Flag Submission
introduces the Modern REST Framework XXE challenge. The task hints that modern APIs—especially those handling JSON—may still accept XML inputs if not properly restricted, making them vulnerable to XXE attacks. The user is instructed to repeat the previous XXE exploitation attempt, this time targeting an endpoint commonly expected to handle JSON, to demonstrate how insecure parsers can still be tricked into processing malicious XML payloads.
![k](https://github.com/user-attachments/assets/a7aa54d8-8c41-4b9f-a2e4-c5f3bf099adf)

---


##  Flag Submission
This image shows a failed attempt to execute an XXE attack within a modern REST framework. The browser's developer tools reveal the server response: "You are posting JSON which does not work with a XXE". This confirms that the endpoint only processes JSON and does not parse XML, effectively mitigating XXE risks. It demonstrates proper server-side input handling and secure parsing configurations that prevent XML-based exploits on JSON endpoints.
![l](https://github.com/user-attachments/assets/f46fb8e1-81e2-4ea6-9e1f-0a44ebec773c)

---

##  Flag Submission
This screenshot captures a JSON-based comment submission attempt via Burp Suite. Although the Content-Type is set to application/json, the request payload ("text": "meooowww") does not demonstrate XML content and therefore cannot exploit XXE. This image reinforces the idea that JSON-only APIs do not parse XML, effectively mitigating XXE attacks unless the server misconfigures its content handling logic.
![m](https://github.com/user-attachments/assets/d7fb3589-9a7f-47b6-a31e-bcf4176cb7e3)

---

##  Flag Submission
This screenshot shows a successful XXE attack performed via XML content submitted to a JSON endpoint that improperly handled the application/xml content type. The attacker crafted a malicious payload using a <!DOCTYPE> declaration referencing an external entity (file:///) and injected it through a comment. The response indicates the lesson was successfully completed, confirming that the vulnerable parser executed the entity expansion, thus demonstrating a real-world risk when parsers fail to restrict external DTDs.
![n](https://github.com/user-attachments/assets/d699e12a-f4e4-48d7-9f58-5eacde008fa4)

---

##  Flag Submission
This screenshot demonstrates a CSRF (Cross-Site Request Forgery) attack attempt where a forged POST request is sent to the /WebGoat/csrf/review endpoint. The attacker tries to submit a fake review (reviewText=meow&stars=2) on behalf of an authenticated user. The inclusion of validateReq with a predictable or static token suggests the endpoint may be vulnerable if proper CSRF tokens are not enforced. Burp Suite is used to intercept and manipulate this request, showing how easily such exploits can be crafted in the absence of CSRF protections.
![o](https://github.com/user-attachments/assets/865ceaa3-3902-4d1b-8a70-4931662f54f0)


---


## Observed Behavior

- The application parses XML input including inline or external DTDs.
- Entities defined in XML are processed and expanded by the parser.
- The parser returns file contents from the local system, confirming that the system is vulnerable to classic XXE.
- Improper handling of DTDs and failure to restrict external entities causes sensitive data leakage.


## Recommended Remediation

- Use anti-CSRF tokens for all form submissions
- Set SameSite attribute on cookies to Strict or Lax
- Enable Secure and HttpOnly flags on session cookies
- Validate the Origin or Referer headers
- Only use POST (not GET) for sensitive actions
- Implement a Content Security Policy (CSP)
- Regularly test the application for CSRF vulnerabilities


---

## References

- OWASP XXE Guide: https://owasp.org/www-project-top-ten/2017/A4_2017-XML_External_Entities_(XXE)
- CWE-611: https://cwe.mitre.org/data/definitions/611.html
- OWASP WebGoat Project: https://owasp.org/www-project-webgoat/
