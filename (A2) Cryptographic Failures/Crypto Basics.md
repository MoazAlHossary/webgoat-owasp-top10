## Crypto Basics

## Vulnerability Description
This module exposes a range of insecure cryptographic practices commonly found in web applications. These include the use of reversible encoding methods (e.g., Base64 for authentication), weak or outdated hashing algorithms (e.g., MD5, SHA-1), insecure password storage (e.g., unsalted hashes), weak obfuscation techniques (e.g., XOR encoding), and the inclusion of sensitive secrets (e.g., encryption keys or passwords) directly within container images or codebases.


## Steps Taken

## 1. Concept
![intro](https://github.com/user-attachments/assets/76651c5e-61c2-45e1-bc96-7a317845468f)

## 2. Base64 Encoding & Basic Authentication
   Demonstrates how Base64 encoding is used in basic authentication and how credentials can be easily decoded when intercepted.
   ![Step 2](https://github.com/user-attachments/assets/f1f474d6-6efd-4a6a-a1ec-0bbe402f0d03)

   Shows successful extraction of credentials (penmh109:secret) from a Base64-encoded HTTP Authorization header.
   ![Step 3](https://github.com/user-attachments/assets/93d2aba3-c4e7-4493-a0d9-709135855f66)

## 3. Other Encoding
   Introduces various encoding techniques including XOR encoding, which is often misused for password obfuscation.
   ![Step 4](https://github.com/user-attachments/assets/a6dbc82d-2397-4e6d-adf8-9e8c4b5e59b8)
   Use an online XOR decoder to reveal the plaintext password databasepassword from the XOR-encoded string.
   ![Step 5](https://github.com/user-attachments/assets/c14a4b10-97e8-4a7d-8c38-af7716308094)
   ![Step 6](https://github.com/user-attachments/assets/2aa1a433-dad1-4b3a-9cec-ec091db9ad7b)

## 4. Plain Hashing
   ![Step 7](https://github.com/user-attachments/assets/166773da-9837-4798-b4ab-4afa8821ea3f)
   Use a Website like "CrackStation" to reverse the MD5 hash and retrieve the original password password.
   ![Step 8](https://github.com/user-attachments/assets/7e523b66-e698-48f5-a2cc-4a78de6e9004)
   ![Step 9](https://github.com/user-attachments/assets/2fdfef6a-e956-41a5-a692-96c863eb4227)
   ![Step 10](https://github.com/user-attachments/assets/c0f83b9e-8458-4d71-b1fd-4b52070d4be9)


---
## 5. Symmetric & Asymmetric encryption  
<img width="996" alt="5" src="https://github.com/user-attachments/assets/b568fbe4-465d-4866-b438-23d5a5c6ef8b" />

## 6. Signitures  
<img width="998" alt="6" src="https://github.com/user-attachments/assets/cf8091ac-0c25-4134-8fa5-d73e343fccc0" />


## 7. RSA Key Assignment
   ![Step 11](https://github.com/user-attachments/assets/d0197cc1-1e4b-4997-b529-f0fe51e8cbaa)
   The provided RSA private key is saved into a local .key file for further cryptographic operations.  
   ![Step 12](https://github.com/user-attachments/assets/7f9e8f83-4402-4a91-affb-31c997a8855b)
   Extract the RSA public key from the private key using OpenSSL and verifies the generated .pub file.  
   ![Step 13](https://github.com/user-attachments/assets/29e73951-7b9b-4d96-988c-f97f1a51e66f)
   User calculates the RSA modulus and signs it using SHA256 and the private key.  
   ![Step 14](https://github.com/user-attachments/assets/13fd17a2-bae4-474f-9e5c-d2c68472d2c8)
   The binary signature file is encoded to Base64 format. 
   ![Step 15](https://github.com/user-attachments/assets/eaeb0882-0072-4c62-8365-ba2fb4ec5029)
   ![Step 16](https://github.com/user-attachments/assets/86477f48-076f-4e44-ac28-748294f2a6bc)

---
## 8. Keystores
<img width="1015" alt="8" src="https://github.com/user-attachments/assets/88b5d6d8-11fa-422f-94aa-383771b8c05c" />

  
## 9. Docker Assignment
the username 'tom' into 'mot', appended similar pattern text, converted to hex, then base64 encoded.
   ![Step 17](https://github.com/user-attachments/assets/aa3af3fe-8b00-43ff-8e4a-7b93dc45ae66)  
   The webgoat/assignments:findthesecret Docker image is pulled to access the password file.  
   ![Step 18](https://github.com/user-attachments/assets/9e855be9-9b7f-4961-8396-07271ed2e2a9)
   The user enters the Docker container as root to access internal files.    
   ![Step 19](https://github.com/user-attachments/assets/ba43557d-26dd-45a9-bde9-2277826e3ab2)
   Navigates to /root and reveals default_secret containing the decryption password.  
   ![Step 20](https://github.com/user-attachments/assets/f2e00077-9797-4a93-b75f-ac98ab1946c2)
   The encrypted message is decrypted using the password file via OpenSSL, revealing the plaintext.  
   ![Step 21](https://github.com/user-attachments/assets/a2f0ff15-6488-4f4e-b940-2f587c162b31)
   
   ![Step 22](https://github.com/user-attachments/assets/2efaf8be-4c2e-443a-8d37-e79b601eb79a)

---

## 10. Post Quantum Cryptography
<img width="1013" alt="10" src="https://github.com/user-attachments/assets/59640fe2-72bb-43e7-8257-8ea7aa6897dc" />

## Observed Behavior
- Base64-encoded credentials were trivially decoded, exposing usernames and passwords in HTTP Authorization headers.

- XOR-encoded passwords were easily reversed using freely available online tools.

- Plain and unsalted hashes were cracked using online hash databases like CrackStation, revealing the original plaintext passwords.

- Private RSA keys were used to derive public keys and generate digital signatures, showcasing improper key handling in exercises.

- Sensitive secrets (e.g., default_secret) were hardcoded into a Docker container image and used to decrypt messages with OpenSSL, highlighting the risk of secret exposure in containerized environments.

---

## Remediation Recommendation

- Avoid using encoding (e.g., Base64) for authentication or security; use proper encryption mechanisms with secure transport protocols (TLS).
- Use strong and modern hashing algorithms such as bcrypt, Argon2, or PBKDF2 for password storage with sufficient salting.
- Eliminate XOR or custom encoding schemes for securing secrets and use industry-standard encryption libraries and algorithms.
- Securely manage private keys and never expose them in client-side environments or publicly accessible repositories.
- Remove hardcoded secrets from container images and use secret management solutions (e.g., HashiCorp Vault, Docker Secrets, AWS Secrets Manager).

---

## References
- OWASP Password Storage Cheat Sheet: https://cheatsheetseries.owasp.org/cheatsheets/Password_Storage_Cheat_Sheet.html
- CrackStation Password Cracking: https://crackstation.net/
- WebSphere XOR Decoder: https://www.axxius.nl/xorpass.html
- Docker Secrets Management: https://docs.docker.com/engine/swarm/secrets/
- NIST SP 800-63B: Digital Identity Guidelines – Authentication & Lifecycle Management: https://pages.nist.gov/800-63-3/sp800-63b.html
- OpenSSL Documentation: https://www.openssl.org/docs/
"""
