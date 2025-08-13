# Task 1 - Basic Pod

## Contents

- [Task 1 - Basic Pod](#task-1---basic-pod)
  - [Contents](#contents)
  - [Assignment](#assignment)
  - [Example commands](#example-commands)
  - [Links](#links)

## Assignment

1. Create Pod with nginx
2. Port-forward Pod port to local machine
3. Probe nginx Pod with curl
4. Cleanup and remove resources

## Example commands

Launch Pod

```bash
kubectl run nginx-pod --image=nginx --port=8443
```

Launch Pod (via Yaml definition)

```bash
kubectl apply -f - <<EOF
apiVersion: v1
kind: Pod
metadata:
  name: nginx-pod
spec:
  containers:
  - name: nginx
    image: nginx
    ports:
    - containerPort: 80
EOF
```

Check Nginx Pod is running

```bash
# Check pod status
kubectl get pods

# Get detailed pod information
kubectl describe pod nginx-pod

# Check pod logs
kubectl logs nginx-pod

# Execute commands inside the pod
kubectl exec -it nginx-pod -- /bin/bash
```

Port-forward Nginx to local machine

```bash
# Port forward to access nginx locally
kubectl port-forward nginx-pod 8080:80
```

Test that Nginx is working

```bash
# Test nginx is running (from another terminal after port-forward)
curl localhost:8080
```

Delete running Pod

```bash
kubectl delete pod nginx-pod
```

## Links

- https://kubernetes.io/docs/concepts/workloads/pods/
- https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#run
- https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#port-forward
