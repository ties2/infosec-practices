
# IAM: Multi-Factor Authentication (MFA) Bypass

**Objective**: Investigate a session hijacking incident bypassing MFA and harden IAM configurations to prevent recurrence.

**Difficulty**: 8/9  
**Time**: 50 minutes

## Steps

1. **Review Logs**  
   - Examine authentication logs (e.g., Okta) for logins that skipped the MFA prompt, indicating a potential bypass.

2. **Spot Hijack**  
   - Identify session token reuse by checking for the same `sessionId` appearing from a new, unauthorized IP address.

3. **Trace Attack**  
   - Correlate authentication logs with network logs to confirm the attacker stole a session cookie after MFA was completed.

4. **Harden**  
   - Reduce session timeout to limit the window of opportunity (e.g., set to 15 minutes in IAM settings).

5. **Add Headers**  
   - Configure application settings to enable `HTTPOnly` and `Secure` flags on session cookies to prevent client-side access and ensure transmission over HTTPS.

6. **Test**  
   - Simulate a login attempt and verify that MFA re-prompts when the IP address changes, confirming the fix.

## Solution

The session timeout was reduced to 15 minutes, and session cookies were secured with `HTTPOnly` and `Secure` flags to prevent future MFA bypass via session hijacking.
