
# Web Log Analysis: Command Injection Exploit

**Objective**: Investigate a command injection exploit in Tomcat logs and implement input validation to prevent further attacks.

**Difficulty**: 7/9  
**Time**: 35 minutes

## Steps

1. **Load Logs**  
   - Open the Tomcat `catalina.out` log file and search for command injection indicators, such as `;`:  
     ```bash
     grep ";" catalina.out
     ```

2. **Find Exploit**  
   - Identify malicious requests, e.g., `GET /app?cmd=whoami;`, where the response reveals sensitive output like `admin`.

3. **Trace**  
   - Confirm the vulnerable endpoint (e.g., `/app`) is processing unsanitized input, allowing command execution.

4. **Fix**  
   - Implement input sanitization in the application code, e.g., using a Java regex to allow only alphanumeric characters:  
     ```java
     if (!input.matches("^[a-zA-Z0-9]+$")) {
         throw new IllegalArgumentException("Invalid input");
     }
     ```

5. **Test**  
   - Resend the malicious request (e.g., `GET /app?cmd=whoami;`) and verify it fails due to input validation.

## Solution

Input validation was added to the `/app` endpoint, blocking command injection attempts by restricting input to alphanumeric characters.
