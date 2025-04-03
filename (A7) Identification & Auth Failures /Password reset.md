## Vulnerability Description

The password reset functionality in many web applications often suffers from logic flaws and insecure design practices. Common issues include revealing whether an account exists, relying on easily guessable or publicly available security questions, and failing to implement brute-force protections or lockout mechanisms. Additionally, some systems send passwords or sensitive reset information via insecure channels like plaintext emails. These flaws collectively allow attackers to enumerate users, guess reset answers, and hijack accounts with minimal resistance.

---

## Steps
![A](https://github.com/user-attachments/assets/f974cb8a-7804-4611-8092-32db90ed61d2)  
Covers common password reset flaws, including logic issues and insecure practices like sending plaintext passwords via email.

![B](https://github.com/user-attachments/assets/2c31bd20-ba49-44e9-8b4e-bb42b3d6938d)  
Demonstrates how password reset messages can unintentionally reveal whether an account exists, enabling attackers to enumerate valid emails.

![C](https://github.com/user-attachments/assets/fa9eafbd-e390-48c6-a27b-aa2f32647178)  
Demonstrates the insecurity of fixed security questions in password resets, which are often guessable or publicly available via social media.

![D](https://github.com/user-attachments/assets/295d9361-7e57-4f5d-9868-c9ee21f219c7)  
Illustrates how an attacker can brute-force security question answers using Burp Suite, highlighting the risk of weak questions and lack of lockout mechanisms.

![E](https://github.com/user-attachments/assets/b0c27566-0111-48cd-9dd1-0d823856dca4)  
Shows Burp Suite’s payload configuration for brute-forcing usernames in password reset security question exploitation.

![F](https://github.com/user-attachments/assets/d939c0f1-bee2-4de0-b5c8-55d4f5945e1c)  
Displays a list of color payloads used in a brute-force attack to guess answers to the security question "What is your favorite color?".

![G](https://github.com/user-attachments/assets/8716a9f2-b222-4a1c-a79d-0b424b497158)  
Brute-force attack using Burp Suite's Intruder successfully guessed the correct combination of username ("admin") and security answer ("green"), completing the lesson and exposing the weakness of relying on guessable security questions.

![H](https://github.com/user-attachments/assets/acd03a8f-afe6-4177-90dc-0ec3bf3b8044)  
Succces! 

![I](https://github.com/user-attachments/assets/edca0a9d-4abc-4498-a7d1-caf7d6c26fba)  
Highlights why certain common security questions—like childhood address—are insecure, as answers may be easily found on social media or could still match a user’s current address.

![J](https://github.com/user-attachments/assets/0fb305ce-7118-46e0-b70e-709d06695dad)  

Covers defensive strategies to prevent abuse of the password reset function, including stronger verification methods, minimizing data exposure, secure tokens, and monitoring user behavior.

---

## Observed Behavior

- **User Enumeration**: Applications responded differently when submitting a valid vs. invalid email in the password reset form, allowing attackers to confirm registered users.
- **Weak Security Questions**: Static questions like "What is your favorite color?" or "What was the street you lived on as a child?" were used, with answers often guessable or found via social media.
- **Brute-force Attack Vectors**: No rate limiting or lockout existed, allowing Burp Suite to be used to automate brute-force attacks against security question answers and usernames.
- **Lack of Token Security**: Reset tokens were not shown to expire quickly or be invalidated after use, making token reuse and interception a potential risk.
- **Poor Feedback Messaging**: Feedback on reset attempts was overly specific, aiding attackers in refining their methods.
- **Plaintext Credentials**: Some systems sent passwords directly over email, which exposes them to interception.

---

## Remediation

- **Generic Responses**: Always return uniform messages for password reset requests, regardless of email validity, to prevent user enumeration.
- **Deprecate Security Questions**: Eliminate traditional security questions or ensure they are user-defined and protected. Encourage the use of password managers or alternative verification methods.
- **Brute-force Mitigation**: Implement rate limiting, CAPTCHAs, and account lockout after multiple failed attempts on password reset or question-answer pages.
- **Secure Token Design**: Use cryptographically strong, time-limited tokens for password resets. Tokens should be invalidated immediately after use.
- **Two-Factor Authentication (2FA)**: Require an additional verification factor (e.g., email link + SMS or app code) for all password reset flows.
- **Audit & Logging**: Monitor all reset attempts and security question responses for anomalies, including geolocation mismatches and high failure rates.
- **Avoid Sensitive Data Over Email**: Never send passwords or reset answers via email. Only include a reset link, and ensure it expires quickly.

---

## References

- [OWASP Forgot Password Cheat Sheet](https://cheatsheetseries.owasp.org/cheatsheets/Forgot_Password_Cheat_Sheet.html)  
- [OWASP Choosing and Using Security Questions](https://cheatsheetseries.owasp.org/cheatsheets/Choosing_and_Using_Security_Questions_Cheat_Sheet.html)  
- [Plaintext Offenders (Examples of Insecure Practices)](http://plaintextoffenders.com/)  
- Slack’s approach to consistent messaging (see screenshots)

