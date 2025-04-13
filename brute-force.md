
# Web Log Analysis: Brute Force Attack

**Objective**: Detect a brute force attack in Nginx web server logs and implement rate-limiting to mitigate it.

**Difficulty**: 5/9  
**Time**: 25 minutes

## Steps

1. **Load Logs**  
   - Filter Nginx `access.log` for login attempts:  
     ```bash
     cat access.log | grep "POST /login"
     ```

2. **Count Attempts**  
   - Identify IPs with excessive requests:  
     ```bash
     awk '{print $1}' access.log | sort | uniq -c
     ```
     - Example: IP `203.0.113.1` with 100+ attempts.

3. **Frequency**  
   - Check timestamps to confirm high-frequency attempts, e.g., 10 requests per second.

4. **Mitigate**  
   - Configure Nginx rate-limiting:  
     ```nginx
     limit_req_zone $binary_remote_addr zone=login:10m rate=5r/m;
     ```
     - Apply to the `/login` endpoint in the Nginx configuration:  
       ```nginx
       location /login {
           limit_req zone=login burst=10;
       }
     ```

5. **Apply**  
   - Reload Nginx to activate the changes:  
     ```bash
     nginx -s reload
     ```

## Solution

Rate-limiting was implemented to cap login attempts at 5 per minute, effectively mitigating the brute force attack from IP `203.0.113.1`.
