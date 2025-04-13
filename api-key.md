
# IAM: Compromised API Key Response

**Objective**: Investigate a leaked API key in AWS CloudTrail logs, rotate the key, and implement monitoring to prevent misuse.

**Difficulty**: 7/9  
**Time**: 45 minutes

## Steps

1. **Check Logs**  
   - Access AWS CloudTrail logs and filter for specific services (e.g., `eventSource == s3.amazonaws.com`) to identify API key activity.

2. **Find Usage**  
   - Search for the `accessKeyId` in logs and flag any usage from unusual IPs (e.g., `203.0.113.1`) indicating potential compromise.

3. **Disable Key**  
   - Deactivate the compromised key to prevent further misuse:  
     ```bash
     aws iam update-access-key --access-key-id AKIA... --status Inactive
     ```

4. **Rotate**  
   - Generate a new API key for the affected user:  
     ```bash
     aws iam create-access-key --user-name user1
     ```

5. **Monitor**  
   - Configure a CloudWatch alarm to alert on any usage of the new key, ensuring proactive detection of suspicious activity.

6. **Report**  
   - Document the compromised key ID, actions taken (e.g., disabled, rotated), and the new key ID for reference.

## Solution

The compromised API key was disabled, a new key was generated, and monitoring was established via CloudWatch to detect potential misuse.
