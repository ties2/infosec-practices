
# Kubernetes: Malicious Container Response

**Objective**: Identify, isolate, and replace a crypto-miner container in a Kubernetes cluster, then redeploy a clean version with monitoring.

**Difficulty**: 8/9  
**Time**: 60 minutes

## Steps

1. **Identify**  
   - Detect the malicious pod by checking for high CPU usage:  
     ```bash
     kubectl top pods
     ```
     - Example: Pod `miner-xyz` shows excessive resource consumption.

2. **Isolate**  
   - Prevent further scheduling on the affected node and delete the malicious pod:  
     ```bash
     kubectl cordon <node>
     kubectl delete pod miner-xyz
     ```

3. **Forensics**  
   - Review pod logs to confirm malicious activity, e.g., connections to a mining pool:  
     ```bash
     kubectl logs miner-xyz
     ```

4. **Redeploy**  
   - Update the deployment to use a trusted container image:  
     ```bash
     kubectl apply -f deploy.yaml
     ```
     Example `deploy.yaml`:
     ```yaml
     apiVersion: apps/v1
     kind: Deployment
     metadata:
       name: app-deployment
     spec:
       replicas: 1
       selector:
         matchLabels:
           app: clean-app
       template:
         metadata:
           labels:
             app: clean-app
         spec:
           containers:
           - name: app
             image: trusted-image:latest
     ```

5. **Monitor**  
   - Add resource limits to prevent future abuse:  
     ```yaml
     resources:
       limits:
         cpu: "500m"
         memory: "512Mi"
       requests:
         cpu: "200m"
         memory: "256Mi"
     ```
     - Apply the updated deployment:  
       ```bash
       kubectl apply -f deploy.yaml
       ```

## Solution

The crypto-miner pod `miner-xyz` was removed, the node was isolated, and a clean pod was deployed with resource limits to prevent recurrence.
