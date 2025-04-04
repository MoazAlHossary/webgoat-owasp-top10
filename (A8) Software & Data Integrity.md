# Insecure Deserialization 

## Vulnerability Description

Insecure deserialization vulnerabilities occur when untrusted or manipulated serialized data is accepted by an application and deserialized without proper validation. Attackers can exploit this flaw to execute arbitrary code, perform denial-of-service attacks, or escalate privileges. This typically affects applications using Java, PHP, Python, Ruby, and other languages that support native serialization mechanisms.

Serialized data is meant to store object states or transmit data across services, but when deserialized carelessly, it can result in execution of malicious code embedded within serialized objects.

---


## Steps

### 1. Concept and Goals
![Concept and Goals](https://github.com/user-attachments/assets/8262467d-5226-4c7a-bdd8-97af736cd220)

- Describes the concept of serialization and goals of the lesson: detection and exploitation of deserialization vulnerabilities.

### 2. What is Serialization
![What is Serialization](https://github.com/user-attachments/assets/2112a748-a7c2-4e27-85a5-578c532ca0c8)

- Serialization converts an object into a byte stream for storage or transfer; deserialization restores it. JSON is the most common format now.
- Lists languages affected by native serialization flaws.

### 3. Vulnerable Code
![Vulnerable Code](https://github.com/user-attachments/assets/3de7c479-fcdf-47de-867e-beff61e4b71f)

- Shows an example where deserialization is done using `ObjectInputStream.readObject()` before type safety checks.

### 4. Class With Dangerous Implementation
![Class with Dangerous readObject](https://github.com/user-attachments/assets/cb18530a-6874-485f-8140-5b25647074bb)

- A vulnerable class `VulnerableTaskHolder` has a `readObject()` method that executes system commands using `Runtime.exec()`.

### 5. Creating the Exploit
![Exploit Creation](https://github.com/user-attachments/assets/4d8e6467-be7f-4692-933e-38a3cb18f793)

- An object of `VulnerableTaskHolder` is created with a malicious command, serialized to a byte array as an exploit payload.

### 6. Understanding Gadget Chains
![Gadget Chains](https://github.com/user-attachments/assets/0b7e1817-666e-41e2-9417-51956a063bd9)

- Explains the concept of gadget chains: interconnected classes that trigger one another to execute malicious actions when deserialized.

---


## Observed Behavior

- **Vulnerable Input Streams**: The application reads serialized objects directly from untrusted input streams without validation.
- **Automatic Execution**: When deserialized, attacker-controlled objects trigger `readObject()` or similar methods, which execute code before type casting.
- **Dangerous Code in Classpath**: Presence of classes in the classpath (e.g., `VulnerableTaskHolder`) with dangerous operations in `readObject()` allows arbitrary command execution.
- **Remote Code Execution**: Exploiting deserialization leads to arbitrary commands like `rm -rf somefile` being executed on the server.
- **Gadget Chains**: Complex deserialization chains composed of multiple classes make detection and mitigation harder.

---

## Remediation

- **Avoid Native Serialization**: Use safer formats like JSON, YAML, or Protocol Buffers that do not support code execution.
- **Implement Validation**: Validate serialized input before deserialization, including type restrictions.
- **Use Object Input Filters**: In Java, use object input filters (`ObjectInputFilter`) to whitelist safe classes.
- **Isolate Deserialization Logic**: Avoid deserializing data from untrusted sources in the main application context.
- **Patch and Monitor**: Keep libraries up to date and monitor deserialization behaviors using security tools.
- **Disable `readObject()`**: If possible, do not implement `readObject()` in ways that execute dangerous logic.

---

## References

- [OWASP Deserialization Cheat Sheet](https://cheatsheetseries.owasp.org/cheatsheets/Deserialization_Cheat_Sheet.html)
- [OWASP A8:2021 - Software and Data Integrity Failures](https://owasp.org/Top10/A08_2021-Software_and_Data_Integrity_Failures/)
- [Java Deserialization Vulnerabilities](https://www.baeldung.com/java-deserialization)

---
