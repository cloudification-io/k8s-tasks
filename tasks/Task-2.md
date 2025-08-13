# Task 2 - Basic DaemonSet

## Contents

- [Task 2 - Basic DaemonSet](#task-2---basic-daemonset)
  - [Contents](#contents)
  - [Assignment](#assignment)
  - [Example commands](#example-commands)
  - [Cleanup resources](#cleanup-resources)
  - [Links](#links)

## Assignment

1. Create DaemonSet with Nginx
2. Check list of Pods
3. Curl to any Pod

## Example commands

Launch DaemonSet

```bash
kubectl create daemonset nginx-daemonset --image=nginx
```

Launch DaemonSet (via YAML)

```bash
kubectl apply -f - <<EOF
apiVersion: apps/v1
kind: DaemonSet
metadata:
  name: nginx-daemonset
  labels:
    app: nginx-daemon
spec:
  selector:
    matchLabels:
      app: nginx-daemon
  template:
    metadata:
      labels:
        app: nginx-daemon
    spec:
      containers:
      - name: nginx
        image: nginx
        ports:
        - containerPort: 80
EOF
```

Check DaemonSet is running

```bash
# Check DaemonSet status
kubectl get daemonset

kubectl describe daemonset nginx-daemonset

kubectl get pods -l app=nginx-daemon -o wide
```

Use port-foward like in previous task to check Nginx is responding to requests

*Extra commands to see running Pods*

```bash
# List pods with more details (wide output)
kubectl get pods -o wide

# List only DaemonSet pods by label
kubectl get pods -l app=nginx-daemon

# Show pods with node information
kubectl get pods -o wide --show-labels

# Get pods across all namespaces
kubectl get pods --all-namespaces
```

## Cleanup resources

```bash
kubectl delete daemonset nginx-daemonset
```

## Links

- https://kubernetes.io/docs/concepts/workloads/controllers/daemonset/
- https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#create
- https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#port-forward
