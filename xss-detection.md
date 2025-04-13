
# Web Log Analysis: Cross-Site Scripting (XSS) Detection

**Objective**: Identify a reflected Cross-Site Scripting (XSS) attack in IIS logs and implement a Content Security Policy (CSP) to mitigate it.

**Difficulty**: 6/9  
**Time**: 30 minutes

## Steps

1. **Load Logs**  
   - Search IIS logs for XSS indicators, such as `<script>` tags:  
     ```bash
     grep "<script>" u_ex*.log
     ```

2. **Spot Payload**  
   - Identify malicious requests, e.g., `GET /search?q=<script>alert(1)</script>`, indicating a reflected XSS attempt.

3. **Confirm**  
   - Verify the server response includes the unescaped payload, confirming the vulnerability.

4. **CSP**  
   - Add a Content Security Policy header to restrict script execution:  
     ```http
     Content-Security-Policy: script-src 'self';
     ```
     - Configure this in the IIS web server or application settings.

5. **Test**  
   - Resend the malicious request and confirm the browser blocks the `<script>` payload due to the CSP.

## Solution

A Content Security Policy was implemented, restricting script execution to trusted sources and preventing the reflected XSS attack.
