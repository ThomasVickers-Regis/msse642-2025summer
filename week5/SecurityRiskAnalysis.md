# Week 5 Security Risk Analysis

## Security Logging and Monitoring Failures

### Introduction & Description
Security Logging and Monitoring Failures occur when an organization fails to adequately log critical security events and fails to actively monitor those logs for suspicious activity. Without effective logging and monitoring, defenders are essentially blind to what is happening within their systems. Attackers can operate undetected for long periods, accessing sensitive data, escalating privileges, and establishing persistence. The inability to detect an ongoing attack in a timely manner significantly increases the potential damage of a breach and makes post-incident forensic investigations nearly impossible.

For example, an application might not log high-risk events like failed login attempts, password resets, or access control failures. Even if it does log these events, the failure occurs if no one is monitoring the logs or if there are no automated alerts set up to flag suspicious patterns, such as thousands of failed logins from a single IP address in a short period. This lack of visibility allows attackers to conduct brute-force attacks, credential stuffing, and other malicious activities without triggering any defensive response.

### Specific Real-World Example
The massive Equifax data breach in 2017 is a textbook example of catastrophic security logging and monitoring failures. While the initial entry point for the attackers was a vulnerability in an Apache Struts component, a critical failure in monitoring allowed the attackers to remain undetected in Equifax's network for 76 days. During this time, the attackers were able to move laterally through the network and exfiltrate the sensitive personal data of over 147 million people.

The failure was twofold. Firstly, Equifax had a device responsible for inspecting network traffic for suspicious activity, but a misconfiguration caused it to stop functioning for months, meaning encrypted traffic was not being inspected. Secondly, this lack of monitoring meant that nobody noticed the large-scale data exfiltration as it was happening. If proper logging and alert systems had been in place to flag anomalous data transfers or suspicious command execution on their servers, the breach could have been detected and stopped much earlier, drastically limiting the scope of the damage. This case clearly shows that simply having security tools is not enough; they must be correctly configured and continuously monitored.

### Analysis About How to Prevent
Preventing security logging and monitoring failures requires a proactive and systematic approach. Organizations must first ensure that all critical security events are logged. This includes events such as:
- Authentication attempts (successful and failed)
- Access control failures
- Server-side input validation failures
- High-value transactions
- Administrative actions
- System configuration changes
- Network traffic anomalies
- Data access and modification events

Logs should be generated in a consistent format and include sufficient detail to understand the context of the event, such as:
- Timestamp
- User/process identifier
- Source IP address
- Event type and severity
- Resource or function being accessed
- Outcome of the event
- Relevant system state

Once logs are being generated, they must be protected from tampering or unauthorized access. This is typically achieved by:
1. Shipping logs to a dedicated, centralized, and secured log management system
2. Implementing log integrity controls
3. Restricting access to log data
4. Maintaining log retention policies
5. Using secure protocols for log transmission

Most importantly, these logs must be actively monitored using:
- Security Information and Event Management (SIEM) systems
- Automated alerting based on predefined rules
- Regular log analysis by security teams
- Threat hunting exercises
- Machine learning-based anomaly detection

### Conclusion
In conclusion, Security Logging and Monitoring Failures create a critical gap in an organization's defense, leaving it vulnerable to prolonged and undetected attacks. As demonstrated by the Equifax breach, a lack of visibility can turn a containable security incident into a catastrophic data breach. The methodology for compromise relies on this blindness, allowing attackers to operate without fear of discovery.

The solution is a comprehensive logging and monitoring strategy. This involves logging all significant security events, protecting the integrity of those logs, and actively monitoring them for suspicious activity using tools like SIEMs and dedicated security teams. By establishing this visibility, organizations can dramatically improve their ability to detect threats, respond to incidents swiftly, and conduct effective forensic analysis, thereby strengthening their overall security posture.

### Verification Sources:
- [Equifax Data Breach Settlement](https://www.ftc.gov/enforcement/cases-proceedings/refunds/equifax-data-breach-settlement)
- [OWASP Logging Cheat Sheet](https://cheatsheetseries.owasp.org/cheatsheets/Logging_Cheat_Sheet.html)
- [NIST Special Publication 800-92: Guide to Computer Security Log Management](https://nvlpubs.nist.gov/nistpubs/Legacy/SP/nistspecialpublication800-92.pdf)

### Prompt
---
*Generated using Gemini 2.5 Pro with the prompt: "Using the requirements from these documents can you format and grammar check my assignment and add any details that are relavent, topic: Security Logging and Monitoring Failures"*