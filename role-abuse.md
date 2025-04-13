
# IAM: Role Assumption Abuse

**Objective**: Detect a user assuming an unauthorized AWS role in CloudTrail logs and restrict the role’s trust policy to prevent abuse.

**Difficulty**: 6/9  
**Time**: 40 minutes

## Steps

1. **Check Logs**  
   - Review AWS CloudTrail logs and filter for `AssumeRole` events to identify role assumption activity.

2. **Find Abuse**  
   - Identify unauthorized actions, e.g., `user1` assuming `arn:aws:iam::123:role/admin`, which isn’t permitted by their policy.

3. **Inspect Trust**  
   - Examine the role’s trust policy to verify why the assumption was allowed:  
     ```bash
     aws iam get-role --role-name admin
     ```

4. **Fix Trust**  
   - Update the trust policy to restrict role assumption to specific, authorized users:  
     ```bash
     aws iam update-assume-role-policy --role-name admin --policy-document file://trust-policy.json
     ```
     Example `trust-policy.json`:
     ```json
     {
       "Version": "2012-10-17",
       "Statement": [
         {
           "Effect": "Allow",
           "Principal": { "AWS": "arn:aws:iam::123:user/authorized-user" },
           "Action": "sts:AssumeRole"
         }
       ]
     }
     ```

5. **Test**  
   - Attempt to assume the role as `user1` to confirm the restriction:  
     ```bash
     aws sts assume-role --role-arn arn:aws:iam::123:role/admin --role-session-name test
     ```
     The command should fail.

## Solution

The trust policy for the `admin` role was tightened to exclude `user1`, preventing unauthorized role assumption.
