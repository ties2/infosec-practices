# Simulate a Full Incident Response Using Network Logs and Endpoint Data

**Objective**: Analyze network logs and endpoint data to trace a security incident, contain it, eradicate the threat, and develop a remediation plan.

**Difficulty**: 7/9  
**Time**: 80 minutes

## Steps

1. **Gather Data**  
   - Collect provided PCAP files (network traffic) and event logs (endpoint data) for analysis.

2. **Trace Impact**  
   - In Wireshark, filter for command-and-control (C2) IP (e.g., `ip.addr == 192.168.1.100`) to identify affected hosts.  
   - Review endpoint logs for malicious process creation (e.g., `malware.exe`).

3. **Identify Scope**  
   - List compromised systems (e.g., IP1, IP2).  
   - Identify affected files (e.g., encrypted documents).

4. **Contain**  
   - Simulate blocking C2 IPs on a firewall (e.g., `iptables -A INPUT -s 192.168.1.100 -j DROP`) to halt communication.

5. **Eradicate**  
   - Remove malware artifacts (e.g., delete `malware.exe`).  
   - Revert malicious changes (e.g., registry modifications).

6. **Recover**  
   - Restore affected systems from backups (assume backups are available).  
   - Patch vulnerabilities, such as updating email filters to prevent recurrence.

7. **Remediation Plan**  
   - Block indicators of compromise (IOCs) on network defenses.  
   - Enforce multi-factor authentication (MFA) across systems.  
   - Draft a phishing awareness email to educate users.

## Solution

Two systems were compromised. The C2 IP was blocked, malware was removed, systems were restored, and users were trained on phishing awareness to prevent future incidents.
