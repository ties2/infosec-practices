# Analyze PCAP and Firewall Logs to Detect Exfiltration

**Objective**: Identify data exfiltration by analyzing PCAP and firewall logs, then mitigate the issue.

**Difficulty**: 6/9  
**Time**: 60 minutes

## Steps

1. **Load PCAP**  
   - Open the PCAP file in Wireshark.  
   - Filter for large outbound transfers (e.g., `http.response` or `ftp-data`).

2. **Spot Anomalies**  
   - Look for unusual destination IPs (e.g., `203.0.113.1`) or high byte counts indicating potential exfiltration.

3. **Check Logs**  
   - Correlate PCAP findings with firewall logs (e.g., `src=192.168.1.10 dst=203.0.113.1 bytes=10MB`) to confirm suspicious activity.

4. **Identify Source**  
   - Trace the internal source IP (e.g., `192.168.1.10`) to the affected host.

5. **Confirm Data**  
   - Extract a sample from the PCAP (e.g., follow TCP stream in Wireshark).  
   - Determine if sensitive data was exfiltrated (e.g., customer database).

6. **Mitigate**  
   - Block the destination IP on the firewall to stop further exfiltration.  
   - Investigate the source host for malware or compromise.

7. **Report**  
   - Document the source and destination IPs, data volume, and mitigation actions taken.

## Solution

10MB of data was exfiltrated from `192.168.1.10` to `203.0.113.1`. The destination IP was blocked, and the source host was scanned for malware.
