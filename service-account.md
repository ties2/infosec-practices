
# IAM: Misconfigured Service Account

**Objective**: Audit a Kubernetes service account with excessive permissions and restrict it using RBAC.

**Difficulty**: 6/9  
**Time**: 35 minutes

## Steps

1. **List Accounts**  
   - Retrieve all service accounts in the cluster:  
     ```bash
     kubectl get serviceaccounts -A
     ```

2. **Check Roles**  
   - Inspect role bindings to identify accounts tied to excessive permissions, such as `cluster-admin`:  
     ```bash
     kubectl describe rolebinding
     ```

3. **Verify Excess**  
   - Test the service account’s permissions to confirm it has overly broad access (e.g., returns “yes” for all actions):  
     ```bash
     kubectl auth can-i --as=system:serviceaccount:namespace:sa-name *
     ```

4. **Edit RBAC**  
   - Create a new `Role` with limited permissions (e.g., allow `get` on `pods` only):  
     ```bash
     kubectl apply -f role.yaml
     ```
     Example `role.yaml`:
     ```yaml
     apiVersion: rbac.authorization.k8s.io/v1
     kind: Role
     metadata:
       namespace: namespace
       name: pod-reader
     rules:
     - apiGroups: [""]
       resources: ["pods"]
       verbs: ["get", "list"]
     ```

5. **Rebind**  
   - Update the `RoleBinding` to associate the service account with the new `Role`:  
     ```bash
     kubectl apply -f rolebinding.yaml
     ```
     Example `rolebinding.yaml`:
     ```yaml
     apiVersion: rbac.authorization.k8s.io/v1
     kind: RoleBinding
     metadata:
       namespace: namespace
       name: pod-reader-binding
     subjects:
     - kind: ServiceAccount
       name: sa-name
       namespace: namespace
     roleRef:
       kind: Role
       name: pod-reader
       apiGroup: rbac.authorization.k8s.io
     ```

6. **Test**  
   - Recheck permissions to ensure the service account is restricted:  
     ```bash
     kubectl auth can-i --as=system:serviceaccount:namespace:sa-name *
     ```
     Should now show limited actions.

## Solution

The service account was restricted to read-only access for pods, removing excessive permissions previously granted by a misconfigured RBAC policy.
