# infosec-practices
# Information Security Assignments

This repository contains a collection of 20 practical, technical assignments designed to simulate real-world information security scenarios. These exercises cover **Incident Response**, **Identity and Access Management (IAM)**, **Web Log Analysis**, **Python Scripting**, and **Kubernetes Security**. Each assignment includes a detailed task description, difficulty level, estimated time, and step-by-step solution process.

The goal is to provide hands-on practice for skills relevant to information security roles, inspired by common interview labs and challenges.

## Structure
Assignments are organized into five categories:
- **[Incident Response](#incident-response)**: Phishing, ransomware, and exfiltration scenarios.
- **[IAM](#iam)**: Privilege management and security in cloud/Kubernetes environments.
- **[Web Log Analysis](#web-log-analysis)**: Detecting attacks in server logs.
- **[Python Scripting](#python-scripting)**: Automating security tasks with Python.
- **[Kubernetes](#kubernetes)**: Securing containerized environments.

Each assignment is stored in the `assignments/` directory, grouped by category.

## Usage
- Clone the repo: `git clone https://github.com/<your-username>/infosec-assignments.git`
- Navigate to an assignment: `cd assignments/<category>/<assignment>.md`
- Follow the steps in each Markdown file to practice in a lab environment (e.g., VirtualBox, AWS, Minikube).
- Tools recommended: Wireshark, `kubectl`, Python, AWS CLI, etc.

## Assignments

### Incident Response
1. [Phishing Email Analysis - Part 1](assignments/incident-response/phishing-part1.md)
2. [Phishing Email Analysis - Part 2](assignments/incident-response/phishing-part2.md)
3. [Phishing Email Analysis - Part 3](assignments/incident-response/phishing-part3.md)
4. [Ransomware Outbreak](assignments/incident-response/ransomware.md)
5. [Data Exfiltration Detection](assignments/incident-response/exfiltration.md)

### IAM
6. [Privilege Escalation Investigation](assignments/iam/privilege-escalation.md)
7. [Misconfigured Service Account](assignments/iam/service-account.md)
8. [Compromised API Key Response](assignments/iam/api-key.md)
9. [MFA Bypass](assignments/iam/mfa-bypass.md)
10. [Role Assumption Abuse](assignments/iam/role-abuse.md)

### Web Log Analysis
11. [SQL Injection Attempt](assignments/web-log-analysis/sql-injection.md)
12. [Brute Force Attack](assignments/web-log-analysis/brute-force.md)
13. [Command Injection Exploit](assignments/web-log-analysis/command-injection.md)
14. [XSS Detection](assignments/web-log-analysis/xss-detection.md)
15. [Anomalous Traffic Spike](assignments/web-log-analysis/traffic-spike.md)

### Python Scripting
16. [Log Parser for IOCs](assignments/python-scripting/log-parser.md)
17. [File Integrity Checker](assignments/python-scripting/file-integrity.md)
18. [Network Scanner for Open Ports](assignments/python-scripting/network-scanner.md)
19. [Credential Harvester Detector](assignments/python-scripting/cred-harvester.md)
20. [Automated Incident Report Generator](assignments/python-scripting/incident-report.md)

### Kubernetes
21. [Pod Privilege Escalation](assignments/kubernetes/pod-escalation.md)
22. [Exposed Dashboard Exploit](assignments/kubernetes/dashboard-exploit.md)
23. [Malicious Container Response](assignments/kubernetes/malicious-container.md)
24. [RBAC Misconfiguration Audit](assignments/kubernetes/rbac-audit.md)
25. [Network Policy Enforcement](assignments/kubernetes/network-policy.md)

## Contributing
Feel free to fork this repo, add your own solutions, or suggest improvements via pull requests!

## License
[MIT License](LICENSE) - Free to use and modify.
