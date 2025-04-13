# IAM: Privilege Escalation Investigation

**Objective**: Analyze AWS CloudTrail logs to identify a user escalating privileges and revoke excessive permissions.

**Difficulty**: 7/9  
**Time**: 40 minutes

## Steps

1. **Load Logs**  
   - Open CloudTrail JSON logs in a text editor or the AWS Management Console.

2. **Filter Events**  
   - Search for privilege escalation-related actions, such as `AssumeRole` or `UpdatePolicy`.

3. **Spot Escalation**  
   - Identify suspicious activity, e.g., a user (e.g., `user1`) attaching the `AdministratorAccess` policy.

4. **Verify Role**  
   - Check the user’s original IAM policy to confirm it shouldn’t allow such actions (e.g., limited to `ReadOnly`).

5. **Revoke**  
   - Remove excessive permissions using AWS CLI:  
     ```bash
     aws iam detach-user-policy --user-name user1 --policy-arn arn:aws:iam::aws:policy/AdministratorAccess

## Fix Policy
Update the user’s IAM policy to explicitly deny iam:* actions to prevent future escalations.

## Log
Document the user, the escalation action, and the remediation steps taken.

## Solution
The user user1 escalated privileges due to a misconfigured IAM policy. Excessive permissions were revoked, and the policy was updated to prevent recurrence.
