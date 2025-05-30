# Week 3 Security Risk Analysis

## Cryptographic Failures

### Introduction & Description
Cryptographic Failures, previously known as "Sensitive Data Exposure," encompass risks related to the inadequate protection of data both in transit and at rest. These failures occur when cryptography is missing, applied incorrectly, or when weak cryptographic algorithms or keys are used, making sensitive information vulnerable to unauthorized access or modification. Such data can include passwords, credit card numbers, health records, personal identifiable information (PII), and business secrets. The impact of cryptographic failures can be severe, leading to identity theft, financial fraud, reputational damage, and regulatory penalties.

A common example of a cryptographic failure is the use of a deprecated or weak hashing algorithm like MD5 or SHA1 for storing passwords. If an attacker gains access to a database of password hashes stored using MD5, they can use readily available rainbow tables or brute-force techniques to quickly recover the original passwords. Another example is transmitting sensitive data over HTTP instead of HTTPS, exposing the data to interception. Similarly, improper key management, such as hardcoding encryption keys in source code or using default keys, drastically undermines the security provided by encryption.

### Specific Real-World Example
A significant real-world example of cryptographic failures contributing to a data breach was the Ashley Madison breach in 2015. The dating website, which catered to individuals seeking extramarital affairs, suffered a massive data breach where hackers released highly sensitive user data, including names, email addresses, sexual preferences, and credit card transaction details. Investigations into the breach revealed several cryptographic weaknesses. One major issue was their password storage mechanism. While they used bcrypt, a strong hashing algorithm, for some passwords, reports indicated that many passwords were also hashed with the much weaker MD5 algorithm, making them easier to crack.

This inconsistency and the use of a weak algorithm for a significant portion of user credentials exemplified a critical cryptographic failure. The exposure of such personal and sensitive information had profound consequences for millions of users, leading to public shaming, extortion attempts, and severe personal repercussions. The Ashley Madison case underscores how failures in implementing cryptography correctly can lead to devastating breaches, even if some stronger cryptographic measures are present elsewhere in the system.

### Analysis About How to Prevent
Preventing cryptographic failures requires a comprehensive strategy focusing on data classification, strong cryptographic practices, and secure key management. Firstly, organizations must identify and classify sensitive data to understand what needs protection and the level of protection required. Once identified, all sensitive data at rest should be encrypted using strong, industry-standard encryption algorithms like AES-256. Data in transit must be protected using protocols like TLS (Transport Layer Security) with up-to-date configurations, ciphers, and server certificates to prevent eavesdropping or man-in-the-middle attacks. It's critical to ensure that encryption is enabled by default and enforced for all sensitive communications.

Effective key management is paramount. This includes using strong, randomly generated keys, storing keys securely (e.g., in a hardware security module (HSM) or a dedicated key management service), regularly rotating keys, and strictly controlling access to them. Deprecated or weak cryptographic algorithms and protocols (e.g., MD5, SHA1, SSLv3, early TLS versions) must be avoided and replaced with current, vetted standards. Furthermore, developers should not attempt to invent their own cryptographic algorithms or protocols ("don't roll your own crypto"), as secure cryptography is notoriously difficult to design correctly. Instead, they should rely on well-vetted, publicly scrutinized libraries and algorithms. Regular security audits and penetration testing can help identify and remediate cryptographic weaknesses.

### Conclusion
In conclusion, cryptographic failures represent a critical vulnerability category where the improper application or absence of cryptographic protections exposes sensitive data. These failures can manifest as the use of weak algorithms, flawed key management, or the transmission of unencrypted data, leading to severe consequences such as data breaches, as highlighted by the Ashley Madison incident where weak password hashing contributed to massive personal data exposure.

The methodology to prevent these failures involves a robust approach: classifying data to determine protection needs, employing strong, up-to-date encryption for data at rest and in transit, and implementing rigorous key management practices. By adhering to industry best practices, avoiding weak or custom cryptography, and regularly auditing systems, organizations can significantly reduce the risk of cryptographic failures and protect sensitive information from unauthorized access.

### Verification Sources
- [Ashley Madison Data Breach](https://en.wikipedia.org/wiki/Ashley_Madison_data_breach)
- [Timeline: Ashley Madison Hack](https://www.digitalguardian.com/blog/timeline-ashley-madison-hack)
- [Ashley Madison Revisited: Legal, Business, and Security Repercussions](https://www.infosecinstitute.com/resources/news/ashley-madison-revisited-legal-business-and-security-repercussions/)
- [The Ashley Madison Data Dump Explained](https://www.nytimes.com/2015/08/20/technology/the-ashley-madison-data-dump-explained.html)

### Prompt
---
*Generated using Gemini 2.5 Pro with the prompt: "Using the requirements from this document can you show me what a good assignment would look like with all important topics covered for this topic: Injection (Cross-Site Scripting)"*