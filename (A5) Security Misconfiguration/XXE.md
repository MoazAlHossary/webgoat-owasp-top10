# OWASP WebGoat - A4: XML External Entities (XXE)


## a. Module Introduction
This lesson introduces XML External Entity (XXE) vulnerabilities, their abuse, and protection mechanisms. The goals are to understand XML structure, XML parser behavior, and how to exploit XXE.

![a](https://github.com/user-attachments/assets/3955d090-7c7d-4ed7-82b3-3b9fe7b11056)

---

## b. XML Entity Basics
Demonstrates how XML parsers resolve internal entities by replacing them with defined values, laying the groundwork for XXE exploitation.
![b](https://github.com/user-attachments/assets/960f2cf2-430c-4722-a69b-db77b5ba33ff)  

Explains how XML input is parsed and shows how XXE vulnerabilities arise when external entities are processed, potentially allowing attackers to exfiltrate sensitive files or conduct internal network scans.
![c](https://github.com/user-attachments/assets/db50eaae-a635-413a-ab9b-917d08c88a9c)

---

## d. External DTD Inclusion Example
Demonstrates how external DTDs and XML entities can be abused to perform XXE attacks, including accessing local files like /etc/passwd by referencing them through the SYSTEM identifier inside a crafted XML payload
![d](https://github.com/user-attachments/assets/8c3f9157-e715-44f6-8741-f5cbfcaa66ab)  

Shows a successful XXE attack where an XML parser loads the contents of /etc/passwd using an external entity. The file content is injected into the XML response, illustrating how a vulnerable parser can leak local files.
![e](https://github.com/user-attachments/assets/0be74acc-6295-4a83-9132-824047e0e67e)

---


## h. Successful XXE Exploit
This image introduces a practical assignment in which the user is prompted to exploit an XXE vulnerability by injecting a malicious payload into the comment field of a photo post, targeting file system disclosure
![h](https://github.com/user-attachments/assets/f9792013-ee32-4b60-87c5-7f658bfb6700)

---

## i. Exploit Payload
 This image shows an initial attempt to exploit the XXE vulnerability by submitting a crafted XML payload through Burp Suite. However, the response indicates failure (lessonCompleted: false) and a feedback message saying the solution is not correct, meaning the payload did not successfully trigger the vulnerability.
![i](https://github.com/user-attachments/assets/5051ef4c-aaca-4bfb-be05-f440ed1a4f2a)

---

## j. Flag Submission
This image shows the successful execution of an XXE attack using Burp Suite. A malicious XML payload was sent containing a DOCTYPE definition with an external entity referencing a file (e.g., /). The server responded with a success message (lessonCompleted: true) and confirmed completion of the XXE assignment, indicating the vulnerability was exploited correctly.
![j](https://github.com/user-attachments/assets/2569e62c-305b-4463-a0f1-cb6cbb28810b)

---

## Observed Behavior

- The application parses XML input including inline or external DTDs.
- Entities defined in XML are processed and expanded by the parser.
- The parser returns file contents from the local system, confirming that the system is vulnerable to classic XXE.
- Improper handling of DTDs and failure to restrict external entities causes sensitive data leakage.

---

## Vulnerability Description

**XML External Entity (XXE)** is a vulnerability that allows an attacker to interfere with an application’s XML processing. It can lead to data exposure, internal file disclosure, server-side request forgery, or even code execution. The root cause is the insecure configuration of XML parsers which allow external entities to be defined and resolved.

---

## References

- OWASP XXE Guide: https://owasp.org/www-project-top-ten/2017/A4_2017-XML_External_Entities_(XXE)
- CWE-611: https://cwe.mitre.org/data/definitions/611.html
- OWASP WebGoat Project: https://owasp.org/www-project-webgoat/
