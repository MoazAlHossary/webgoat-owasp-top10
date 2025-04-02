
# OWASP A9: Using Components with Known Vulnerabilities

## Concept & Goals
**Concept**:  
This section introduces the risks associated with the modern software development practice of using open source libraries. As open source adoption continues to grow (with over 4 trillion downloads in 2023), many teams integrate dependencies without verifying their security. This can lead to vulnerabilities being introduced unknowingly.

**Goals**:
- Understand that open source code is as critical as custom-written code.
- Recognize the importance of tracking and managing dependencies.
- Learn about the role of a Software Bill of Materials (SBOM) in evaluating component risks.

![A](https://github.com/user-attachments/assets/8ae0e234-133d-4227-8860-74cb881673a2)

## The Open Source Ecosystems
**Overview**:  
This section outlines the complexity and scale of the open source ecosystem, which includes millions of code and binary repositories. It emphasizes the challenges in validating and managing source code integrity and distribution practices.

![B](https://github.com/user-attachments/assets/7344c7f2-fceb-424b-8782-214171d40f8d)

## 2013 OWASP Top 10
As early as 2013, OWASP identified the use of vulnerable components as a major risk.

**Risk Summary**:
- **Exploitability**: Average — attackers may need customization or deep access.
- **Prevalence**: Widespread — most developers don’t track library versions or dependencies closely.
- **Detectability**: Difficult — vulnerabilities may not be visible or well-documented.
- **Impact**: Moderate — can result in injection, remote code execution, XSS, and full host takeover.
- **Business Impact**: Application specific — can vary from negligible to complete system compromise.

**Prevention Strategies**:
- Maintain an inventory of all components and dependencies.
- Regularly monitor vulnerability databases (e.g., CVE, NVD).
- Apply security policies for component usage and enforce version upgrades.
- Use security wrappers or controls to protect vulnerable libraries.

![C](https://github.com/user-attachments/assets/372e18a9-14d0-414a-ad37-7c766edbbc75)

## Components are Everywhere
Modern applications like WebGoat rely heavily on open-source components, often without fully tracking their risks.

![D](https://github.com/user-attachments/assets/8d6cdb59-849b-4b17-8d30-a017e376047a)

## The Exploit Is Not Always in Your Code
This WebGoat demo shows that different versions of the same library (e.g., jquery-ui) can have dramatically different security implications.

![E](https://github.com/user-attachments/assets/6837283f-6782-4ff8-ab18-315ffdaa792f)

## Knowing the OSS "Bill of Materials"
Understanding which open-source components exist in a project is key to identifying and mitigating their risk.

![F](https://github.com/user-attachments/assets/f3812296-e323-4c51-8d64-38eaee968d1a)

## How Do I Generate a Bill of Materials?
OWASP Dependency-Check helps generate an SBOM and scan components for vulnerabilities. Example usage via Maven plugin is shown.

![G](https://github.com/user-attachments/assets/8d09079c-5122-45f4-a04a-4ed9a74cfb44)  
**Command**: `mvn clean install -Powasp`  
**Report**: `webgoat-container/target/dependency-check-report.html`

![H](https://github.com/user-attachments/assets/aec921af-57f3-4f40-b41b-e9b49f42b1ca)

## Security Information Overload
Too much security information can overwhelm development teams and reduce effectiveness.

![I](https://github.com/user-attachments/assets/6b667a68-90b0-4e18-896e-192e041c842d)

## License Information Overload
Interpreting open source license restrictions is often difficult.

![J](https://github.com/user-attachments/assets/2c34044b-809d-4d24-9308-c24f374572a6)

## Architecture Information
Knowing how outdated a component is helps assess risk more effectively.

![K](https://github.com/user-attachments/assets/63c34402-8d16-4381-9d29-7ea080b418fe)

## Some Examples of Open Source Software (OSS) Risk
![L](https://github.com/user-attachments/assets/7a90b3e4-00fb-43d6-bb93-c147c33f5e0f)

---

## Vulnerability Description
Using outdated, vulnerable components exposes applications to known exploits, including injection attacks, remote code execution, and XSS. Developers often include third-party libraries without assessing their risk, making the attack surface broader and harder to monitor.

---

## Remediation
- Maintain and update a software bill of materials (SBOM).
- Use automated tools like OWASP Dependency-Check to scan dependencies.
- Subscribe to vulnerability feeds (e.g., NVD, CVE lists).
- Avoid using unsupported or deprecated libraries.
- Regularly audit and patch all included open-source components.
- Use secure defaults and apply least privilege principles to included code.

---

## References
- [OWASP A9: Using Components with Known Vulnerabilities](https://owasp.org/www-project-top-ten/2017/A9_2017-Using_Components_with_Known_Vulnerabilities)
- [OWASP Dependency-Check](https://owasp.org/www-project-dependency-check/)
- [SBOM – Software Bill of Materials](https://www.ntia.gov/SBOM)
