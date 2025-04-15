
# Kubernetes: RBAC Misconfiguration Audit

**Objective**: Audit and tighten overly permissive Kubernetes RBAC roles to restrict access.

**Difficulty**: 6/9  
**Time**: 40 minutes

## Steps

1. **List Roles**  
   - Retrieve all role bindings across namespaces:  
     ```bash
     kubectl get rolebindings -A
     ```

2. **Check Perms**  
   - Inspect role bindings for excessive permissions, such as wildcard rules (`*:*`):  
     ```bash
     kubectl describe rolebinding
     ```

3. **Edit Role**  
   - Modify the overly permissive role to limit access, e.g., restrict to `get` on `pods`:  
     ```bash
     kubectl edit role <name>
     ```
     Example updated role:
     ```yaml
     apiVersion: rbac.authorization.k8s.io/v1
     kind: Role
     metadata:
       namespace: <namespace>
       name: <name>
     rules:
     - apiGroups: [""]
       resources: ["pods"]
       verbs: ["get", "list"]
     ```

4. **Test**  
   - Verify the role is restricted using:  
     ```bash
     kubectl auth can-i --as=system:serviceaccount:<namespace>:<sa-name> '*'
     ```
     - Should show limited permissions, e.g., only `get` and `list` for `pods`.

## Solution

The overly permissive role was updated to allow only read access (`get`, `list`) to pods, ensuring tighter RBAC controls.
