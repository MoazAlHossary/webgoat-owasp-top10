# Server-Side Request Forgery


## Vulnerability Description

A Server-Side Request Forgery (SSRF) vulnerability allows an attacker to induce the server-side application to make HTTP requests to an arbitrary domain of the attacker’s choosing. This can expose internal systems and services that are not intended to be accessible externally, and potentially lead to the exposure of sensitive data, internal credentials, or remote code execution.

---

## Step-by-Step Screenshots and Observations

### 1. **SSRF Concept & Goals**
![Concept](https://github.com/user-attachments/assets/9853cbe0-a39e-42b5-b51e-6aa0b7a01a58)
This section introduces the SSRF concept and outlines what students will learn—how to intercept and manipulate server-bound requests.

### 2. **Initial Attack**
![Intercepted Request](https://github.com/user-attachments/assets/4624653c-05fe-4b50-8f41-81ace179c173)
The attacker clicks a button which triggers a server-side fetch. Burp Suite captures the outbound request.

### 3. **Intercept Details**
![Burp Request](https://github.com/user-attachments/assets/cb998760-aa8c-4f0c-a546-262f86a0f3e5)
Original request points to `tom.png`. The attacker identifies and targets the `url=` parameter for manipulation.

### 4. **Payload Modification**
![Modified URL](https://github.com/user-attachments/assets/f2feb874-8453-4f54-9f73-7d53428c7dc5)
Changing the image path to `jerry.png` via URL encoding.

### 5. **Successful Exploit**
![Success Jerry](https://github.com/user-attachments/assets/802ebe91-f12a-4bb0-8d64-b9e885682c06)
Jerry’s image is loaded—indicating the server processed the altered request, confirming SSRF.

### 6. **External Request Challenge**
![External Request](https://github.com/user-attachments/assets/d7043d80-62a3-4ae5-9a90-da95f7482a3b)
User is prompted to modify the request to fetch data from `http://ifconfig.pro`.

### 7. **Modified Burp Request**
![Burp External](https://github.com/user-attachments/assets/4a327d08-2140-435b-9eb7-5374b731cb26)
The `url` parameter is changed to target `http://ifconfig.pro`.

### 8. **Exploit Confirmation**
![Ifconfig Data](https://github.com/user-attachments/assets/f0ca88c4-9d43-462d-a9d3-77bffd26853f)
Server returns IP address and environment details retrieved from the external resource.

### 9. **Preventative Measures**
![Prevention](https://github.com/user-attachments/assets/c2dff449-de48-4e1e-888d-05a21134553e)
The lesson concludes with guidelines on preventing SSRF by restricting server-side fetch behavior, validating input, and whitelisting domains.

---

## Observed Behavior

- The lesson demonstrates how the attacker can manipulate a request URL to access unauthorized resources.
- By intercepting the request with Burp Suite, the attacker identifies the parameter `url=images%2Ftom.png`.
- The attacker then modifies this parameter to point to a different internal or unauthorized resource, such as `jerry.png`.
- Upon submitting the altered request, the application renders a new image and confirms SSRF exploitation.
- Further tasks involve directing the server to fetch data from an external site (e.g., `http://ifconfig.pro`) and successfully retrieving the external server’s IP data.

---

## Remediation

- **Whitelist Validation**: Enforce strict whitelisting of domains, IPs, and protocols that the server is allowed to access.
- **Input Validation**: Validate and sanitize user-supplied input to ensure it matches expected patterns and endpoints.
- **Network Segmentation**: Prevent applications from making arbitrary requests to internal networks or metadata services.
- **Disable URL Fetching When Unnecessary**: Avoid using dynamic URLs controlled by the user whenever possible.
- **Monitoring and Alerting**: Implement proper logging and alerting to monitor unusual outbound traffic from internal systems.

---

## References
- [HackerOne Blog on SSRF](https://www.hackerone.com/blog-How-To-Server-Side-Request-Forgery-SSRF)
