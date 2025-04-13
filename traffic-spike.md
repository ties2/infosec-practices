
# Web Log Analysis: Anomalous Traffic Spike

**Objective**: Analyze a traffic spike in web server logs to identify its cause and propose mitigation strategies.

**Difficulty**: 7/9  
**Time**: 40 minutes

## Steps

1. **Load Logs**  
   - Extract timestamps from `access.log` to identify the spike:  
     ```bash
     awk '{print $4}' access.log | sort | uniq -c
     ```
     - Example: Spike detected at `[03/Apr/2025:10:00]`.

2. **Check Source**  
   - Filter logs for the spike time and analyze source IPs:  
     ```bash
     grep "10:00" access.log | awk '{print $1}' | sort | uniq -c
     ```
     - Result: Multiple IPs with high request counts.

3. **DDoS Check**  
   - Confirm characteristics of a Distributed Denial-of-Service (DDoS) attack: random IPs and high request volume.

4. **Mitigate**  
   - Implement rate-limiting to control traffic:  
     - Option 1: Use Cloudflare rate-limiting to restrict requests per IP.  
     - Option 2: Configure `iptables` on the server:  
       ```bash
       iptables -A INPUT -p tcp --dport 80 -m limit --limit 25/min -j ACCEPT
       ```

5. **Test**  
   - Simulate high-volume traffic to verify excess requests are dropped by the rate-limiting rules.

## Solution

The traffic spike was identified as a DDoS attack and mitigated by implementing rate-limiting to cap requests at 25 per minute per IP.
