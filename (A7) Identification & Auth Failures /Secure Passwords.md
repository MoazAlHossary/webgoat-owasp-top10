# WebGoat A7: Secure Password Storage

##  Vulnerability Description
The A7: Secure Password Storage module focuses on the common security issue of improperly storing user passwords. Many applications still store passwords in plain text, weak hashes, or using outdated practices like fixed salts or security questions. This module follows NIST SP 800-63B guidelines, educating users on modern best practices to create, evaluate, and store secure passwords. It also addresses usability, encouraging practices that increase password strength without sacrificing user experience.

![A](https://github.com/user-attachments/assets/b98d5637-473e-420d-8889-8602a064fe5f)  

![B](https://github.com/user-attachments/assets/e92749a1-46f7-439d-8085-34c098f0eaf9)  
Shown above teaches users how to create strong passwords and store them securely, following NIST guidelines and best practices for password management in applications.

![C](https://github.com/user-attachments/assets/01bac249-41fe-487e-a8c1-36edd37f9eb9)  
![D](https://github.com/user-attachments/assets/6d84f20e-adad-4216-9aa0-5ec04c2ba060)  
The A7 module teaches secure password creation and storage practices based on NIST SP 800-63B guidelines. It covers modern recommendations such as avoiding forced composition rules, allowing Unicode, rejecting breached passwords, and setting a minimum length of 8 characters.
![E](https://github.com/user-attachments/assets/0325637b-c788-4109-a681-51143e3fda74)  
This exercise helps users understand password strength by estimating brute-force cracking time, reinforcing the importance of long, unpredictable passwords for secure storage.
![F](https://github.com/user-attachments/assets/104181de-9a8c-4ca8-a7a6-4da2489aafe0)  
The module emphasizes real-world password hygiene by encouraging practices like using unique passwords per account, generating passphrases, and enabling two-factor authentication. It also recommends checking for exposed credentials using tools like Have I Been Pwned.
![G](https://github.com/user-attachments/assets/2dce65e5-94ac-45be-8e3f-ed66861c0322)  
highlights secure storage practices like encrypting password transmission, salting passwords, and using strong hashing algorithms such as PBKDF2, SHA-3, or HMAC. It also emphasizes using memory-hard functions and high cost factors (≥10,000 iterations) to resist offline attacks.


##  Observed Behavior
Users are presented with interactive lessons that show:
- How to build strong passwords based on length and entropy.
- How brute-force tools estimate cracking time.
- Why common passwords and patterns (e.g., "1234", "password") are weak.
- How weak storage practices (e.g., lack of salting or hashing) can lead to offline attacks.
- The importance of personal hygiene like using unique passwords, passphrases, password managers, and 2FA.
- What secure password storage looks like using PBKDF2, HMAC, and encryption in transit.

##  Remediation
To remediate insecure password storage:
- Store all passwords using strong key derivation functions (PBKDF2, bcrypt, scrypt).
- Salt each password with a unique, randomly generated salt (≥32 bits).
- Use high cost factors (≥10,000 iterations) and memory-hard algorithms where possible.
- Use HTTPS/TLS to protect password transmission.
- Avoid composition rules, password hints, and security questions.
- Allow pasting, password visibility toggles, and strength meters for better UX.
- Screen passwords against breached wordlists using services like Have I Been Pwned.

##  References
- [NIST SP 800-63B Digital Identity Guidelines](https://pages.nist.gov/800-63-3/sp800-63b.html)
- [OWASP Password Storage Cheat Sheet](https://cheatsheetseries.owasp.org/cheatsheets/Password_Storage_Cheat_Sheet.html)
- [Have I Been Pwned](https://haveibeenpwned.com)
- [Diceware Passphrase Generator](https://www.rempe.us/diceware/)
