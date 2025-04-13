# Investigate a Ransomware Incident Using Logs and Artifacts

**Objective**: Analyze logs and artifacts to identify the entry point of a ransomware incident and propose a recovery plan.

**Difficulty**: 7/9  
**Time**: 75 minutes

## Steps

1. **Review Logs**  
   - Examine Windows Event Logs (Security, Application) for anomalies, such as unusual logins (e.g., Event ID 4624).

2. **Find Entry**  
   - Investigate potential entry points, such as RDP brute force attempts (e.g., Event ID 4625) or phishing indicators (e.g., email-related processes in logs).

3. **Analyze Artifacts**  
   - Locate ransomware artifacts, such as a ransom note (e.g., `README.txt`) and encrypted files (e.g., `.locked` extension).

4. **Trace Encryption**  
   - Map affected files using commands like `dir /s *.locked` or by analyzing log timestamps to determine the scope of encryption.

5. **Contain**  
   - Isolate infected hosts by disconnecting them from the network (e.g., disable network adapter).

6. **Recover**  
   - Restore affected systems from offline backups.  
   - Avoid attempting decryption without a verified key to prevent data loss.

7. **Mitigate**  
   - Patch vulnerabilities, such as securing RDP (disable if unused).  
   - Update antivirus signatures to detect future threats.

## Solution

The ransomware entered via an RDP brute force attack, encrypting 50 files. Systems were restored from offline backups, and RDP was secured to prevent recurrence.
