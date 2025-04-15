
# Kubernetes: Network Policy Enforcement

**Objective**: Restrict pod-to-pod traffic in a Kubernetes cluster using network policies to allow only specific communication.

**Difficulty**: 7/9  
**Time**: 45 minutes

## Steps

1. **Check Traffic**  
   - Verify unrestricted pod communication:  
     ```bash
     kubectl exec pod1 -- ping pod2
     ```
     - Confirm ping succeeds, indicating no restrictions.

2. **Create Policy**  
   - Define a network policy to allow traffic only from pods labeled `app=frontend` to `app=backend`:  
     ```bash
     kubectl apply -f netpol.yaml
     ```
     Example `netpol.yaml`:
     ```yaml
     apiVersion: networking.k8s.io/v1
     kind: NetworkPolicy
     metadata:
       name: restrict-traffic
       namespace: default
     spec:
       podSelector:
         matchLabels:
           app: backend
       policyTypes:
       - Ingress
       ingress:
       - from:
         - podSelector:
             matchLabels:
               app: frontend
         ports:
         - protocol: TCP
           port: 8080
     ```

3. **Apply**  
   - Label pods to match the network policy:  
     ```bash
     kubectl label pod pod1 app=frontend
     kubectl label pod pod2 app=backend
     ```

4. **Test**  
   - Retry the ping or traffic test:  
     ```bash
     kubectl exec pod1 -- ping pod2
     ```
     - Confirm traffic is blocked unless it matches the policy (e.g., `frontend` to `backend` on port 8080).

## Solution

Pod-to-pod traffic was restricted using a network policy, allowing only communication from `app=frontend` to `app=backend` pods, blocking unauthorized access.
