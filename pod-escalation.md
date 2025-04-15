
# Kubernetes: Pod Privilege Escalation

**Objective**: Identify and fix a Kubernetes pod with elevated privileges by implementing a Pod Security Policy (PSP) to enforce non-privileged execution.

**Difficulty**: 8/9  
**Time**: 50 minutes

## Steps

1. **Check Pods**  
   - Inspect running pods for privileged configurations:  
     ```bash
     kubectl get pods -o yaml | grep privileged
     ```

2. **Find Issue**  
   - Identify the problematic pod with `securityContext: privileged: true` in its specification.

3. **Create PSP**  
   - Define a Pod Security Policy to deny privileged containers:  
     ```bash
     kubectl apply -f psp.yaml
     ```
     Example `psp.yaml`:
     ```yaml
     apiVersion: policy/v1beta1
     kind: PodSecurityPolicy
     metadata:
       name: restricted-psp
     spec:
       privileged: false
       runAsUser:
         rule: MustRunAsNonRoot
       seLinux:
         rule: RunAsAny
       fsGroup:
         rule: RunAsAny
       supplementalGroups:
         rule: RunAsAny
       volumes:
       - '*'
     ```

4. **Apply**  
   - Bind the PSP to the relevant namespace using a `ClusterRole` and `RoleBinding`:  
     ```bash
     kubectl apply -f psp-binding.yaml
     ```
     Example `psp-binding.yaml`:
     ```yaml
     apiVersion: rbac.authorization.k8s.io/v1
     kind: ClusterRole
     metadata:
       name: use-restricted-psp
     rules:
     - apiGroups: ['policy']
       resources: ['podsecuritypolicies']
       verbs: ['use']
       resourceNames: ['restricted-psp']
     ---
     apiVersion: rbac.authorization.k8s.io/v1
     kind: RoleBinding
     metadata:
       name: restricted-psp-binding
       namespace: default
     subjects:
     - kind: Group
       name: system:authenticated
       apiGroup: rbac.authorization.k8s.io
     roleRef:
       kind: ClusterRole
       name: use-restricted-psp
       apiGroup: rbac.authorization.k8s.io
     ```

5. **Redeploy**  
   - Edit the pod specification to remove `privileged: true` and redeploy:  
     ```bash
     kubectl apply -f pod.yaml
     ```

6. **Test**  
   - Verify the pod runs without privileged escalation and complies with the PSP.

## Solution

A Pod Security Policy was implemented to enforce non-privileged pod execution, and the offending pod was redeployed without elevated privileges.
