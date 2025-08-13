# Task 1 - Fix broken Pod

## Contents

- [Task 1 - Fix broken Pod](#task-1---fix-broken-pod)
  - [Contents](#contents)
  - [Assignment](#assignment)
  - [Example commands](#example-commands)
  - [Cleanup resources](#cleanup-resources)
  - [Links](#links)

## Assignment

1. Apply yaml files
2. Investigate why Pod is not working

## Example commands

Apply manifests via kubectl

```bash
kubectl apply -f pod.yml
```

Another option to apply from web link

```bash
kubectl apply -f <WEB_LINK>
```

Useful troubleshooting commands

```bash
kubectl get pods
kubectl get pod broken-nginx-pod

# Check with more details
kubectl get pod broken-nginx-pod -o wide

# Monitor pod status in real-time
kubectl get pod broken-nginx-pod -w

kubectl describe pod broken-nginx-pod

kubectl logs broken-nginx-pod
```

## Cleanup resources

```bash
kubectl delete pod broken-nginx-pod
```

## Links

- https://kubernetes.io/docs/concepts/configuration/organize-cluster-access-kubeconfig/
