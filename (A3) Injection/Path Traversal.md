# OWASP WebGoat – A3: Cross-Site Scripting (XSS) Mitigation

## Vulnerability Description
Path Traversal, also known as Directory Traversal, is a type of web security vulnerability that allows an attacker to access files and directories stored outside the intended file system path. When user input is used to construct file paths without proper sanitization, attackers can exploit sequences like ../ or its encoded variants to escape the restricted directory and gain unauthorized access to sensitive files.

In this WebGoat module, the application allows users to upload a profile image. However, due to insufficient validation of the file path, attackers can manipulate the upload destination and overwrite files outside the intended upload directory.


---

## 🔹Path Traversal - How does it work?

![a.png](https://github.com/user-attachments/assets/b6b3adef-7fc3-4d66-9e82-ffdd2aa9558f)

---

## 🔹 b.png – Path Traversal Introduction
This screen introduces the Path Traversal challenge, where the objective is to upload a file and overwrite a target file outside the normal upload directory using traversal techniques.
![b.png](https://github.com/user-attachments/assets/5754f8a8-0a0c-4726-bf73-da807fa517ff)

---

## 🔹Upload Confirmation Message
This shows the confirmation message after uploading a profile image. The file path where the uploaded image is stored is shown, revealing the server directory and confirming upload success.
![c.png](https://github.com/user-attachments/assets/1a63a860-c1a7-44e2-ae60-0adda551cb7f)

---

## 🔹Path Traversal via Burp Suite
This Burp Suite request shows the file upload manipulation. The attacker uses `../test` as a filename to perform a path traversal, attempting to upload the file outside the intended directory.
![d.png](https://github.com/user-attachments/assets/14444861-1b35-4872-9592-d76c29caf923)

---

## 🔹Assignment Completion
![e.png](https://github.com/user-attachments/assets/a787384a-7742-45f9-8423-ee1b2e222794)


---

## 🔹Path Traversal Challenge (Sanitization Attempt)
In this updated scenario, developers attempt to sanitize file upload paths by removing `../`, preventing simple directory traversal. The goal remains the same: bypass this fix to overwrite files outside the intended directory.
![f.png](https://github.com/user-attachments/assets/424fa3d1-46e4-4624-bfdc-4a1182edc48d)

---

## 🔹Bypassing Path Traversal Filter
The request demonstrates an attempt to bypass the server-side sanitization by using a more complex traversal pattern (`....//test`). This exploits weak filtering logic that removes exact `../` patterns but overlooks obfuscated variations.
![g.png](https://github.com/user-attachments/assets/822bb279-6c89-4cb9-8a28-49471f0fb201)

---

## 🔹Assignment Completion

![h.png](https://github.com/user-attachments/assets/3203e796-4b9e-44b6-8229-b65c5a4de013)

---


## 🔹Path Traversal Challenge with Updated Filters
The fourth stage of the path traversal module introduces a new fix that validates the `full name` input field more strictly. The challenge is to bypass the newly added filtering mechanism.
![i.png](https://github.com/user-attachments/assets/15f66b02-b7a0-4bdc-9301-3b671fada084)

---

## 🔹Attempt to Bypass Upload Filter via Filename
This Burp Suite capture shows an attempt to exploit path traversal by injecting `../` into the `filename` attribute of the file upload field, bypassing input filters that removed it from user input fields.
![j.png](https://github.com/user-attachments/assets/7e642118-0ec0-452f-9390-6ff4e908034d)

---

## 🔹Assignment Completion
![k.png](https://github.com/user-attachments/assets/05d81546-8ad9-4d14-8213-1183f0285e98)

---

## 🔹Retreving other files with a Path Traversal
![l.png](https://github.com/user-attachments/assets/33d8bcec-b996-4227-a5ff-d153d627829c)

---

## 🔹Path Traversal Blocked Attempt
An attempt to perform path traversal using `../../` in the query parameter results in a 400 Bad Request. The response indicates that illegal characters are not allowed in the query, implying basic input validation or filtering is in place.
![m.png](https://github.com/user-attachments/assets/b802c734-395f-48e9-8930-5e18106fd16f)

---

## 🔹URL Encoding Bypass Attempt
To bypass input filters that block `../`, the path traversal sequence is encoded as `%2e%2e%2f`, which represents `../` in URL encoding. This technique is commonly used to evade naive input validation mechanisms that do not decode encoded values before validation.
![n.png](https://github.com/user-attachments/assets/89cae8ac-52bc-4ecd-a85b-7b706780eb44)

---

## 🔹Enumerating Directory Contents via Encoded Traversal
Using the encoded path traversal payload (`%2e%2e%2f`), the application leaks a list of files in the parent directory. Among them is the target file `path-traversal-secret.jpg`, indicating that directory listing is improperly exposed due to insufficient input sanitization and lack of path normalization.
![o.png](https://github.com/user-attachments/assets/180dfe29-a982-471e-bb93-6000e49f6e15)

---

## 🔹Viewing Network Response for Image Retrieval
The browser's developer tools confirm successful retrieval of the requested image file (`id=1.jpg`) via a `GET` request. The response status is `200 OK`, and the content type is `image/jpeg`, showing how user-controlled parameters directly access image files on the server.
![p.png](https://github.com/user-attachments/assets/9b4f9968-0f56-4e35-83ef-2f949d19dd0c)

---

## 🔹Successful Path Traversal to Secret File
The Burp Suite Repeater shows a successful path traversal attack using double URL encoding. The requested file `path-traversal-secret` is retrieved with a `200 OK` response. The server confirms the attack success and instructs to submit the SHA-512 hash of the username as the answer.
![q.png](https://github.com/user-attachments/assets/213439ec-ae54-4895-9835-f9be57d3ffd4)

## 🔹Assignment Completion
![r.png](https://github.com/user-attachments/assets/ae32f502-2e56-493e-af9f-686f1576d914)

---

### Observed Behavior:
In the vulnerable implementation, the backend does not sufficiently sanitize or restrict the filename parameter in the upload process. The attacker used path traversal techniques such as:

  - ../test
  
  - ....//test
  
  - Double URL encoding: %2e%2e%2f (which decodes to ../)

This allowed the attacker to:

  - Navigate outside the designated upload directory.
  
  - Write files into unintended paths such as configuration directories or sensitive locations.

Despite incremental sanitization attempts by the developers (e.g., stripping ../), the lack of canonicalization checks and encoding decoding still left the application exposed.



---


###  Recommended Remediation

1. **Canonicalize and Sanitize All File Paths:**

   - Normalize paths to remove encoded traversal sequences before using them in file operations.  
   - Reject any file path that attempts to escape the allowed base directory after canonicalization.

2. **Enforce Strict Whitelisting:**

   - Only allow file uploads with trusted extensions and filenames.  
   - Save uploaded files using generated server-side names, not user input.

3. **Implement Upload Path Constraints:**

   - Restrict uploads to a sandboxed directory (e.g., `/uploads/users/`).  
   - Use filesystem APIs to validate that the resolved path is within the allowed directory.

4. **Input Validation and Encoding:**

   - Use secure frameworks or libraries that handle input sanitization and output encoding automatically.  
   - Validate the full content and filename against a secure policy.

5. **Logging & Monitoring:**

   - Log any attempts of path traversal for detection and response.  
   - Monitor the file system for unauthorized modifications.

