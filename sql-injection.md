
# Web Log Analysis: SQL Injection Attempt

**Objective**: Identify SQL injection attempts in Apache web server logs and propose Web Application Firewall (WAF) rules to block them.

**Difficulty**: 6/9  
**Time**: 30 minutes

## Steps

1. **Load Logs**  
   - Open the Apache `access.log` file in a text editor for analysis.

2. **Search Pattern**  
   - Use `grep` to search for common SQL injection keywords:  
     ```bash
     grep "SELECT\|UNION\|'" access.log
     ```
     - Example finding: `GET /page?id=1' UNION SELECT ...`

3. **Extract Payload**  
   - Note the malicious query string and source IP (e.g., `203.0.113.1`) from the log entry.

4. **Intent**  
   - Analyze the payload; use of `UNION` suggests an attempt to extract unauthorized data from the database.

5. **WAF Rule**  
   - Create a ModSecurity rule to block SQL injection attempts:  
     ```apache
     SecRule ARGS "SELECT|UNION" "block,id:1001"
     ```

6. **Test**  
   - Simulate a request containing `SELECT` or `UNION` to ensure the WAF rule triggers and blocks the attempt.

## Solution

A SQL injection attempt was identified and blocked using a ModSecurity WAF rule targeting `SELECT` and `UNION` keywords.
