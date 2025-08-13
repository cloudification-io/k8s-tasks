# Task 6 - 

## Contents

- [Task 6 -](#task-6--)
  - [Contents](#contents)
  - [Assignment](#assignment)
  - [Example commands](#example-commands)
  - [Cleanup resources](#cleanup-resources)
  - [Links](#links)

## Assignment

1. apply with kubectl
2. investigate why Pods are not running

## Example commands

Apply objects via kubectl

```bash
kubectl apply -f deployment.yml
```

Useful debug commands

```bash
kubectl get pods

kubectl get statefulset

kubectl describe pod

kubectl describe statefulset

kubectl get nodes --show-labels

kubectl get events
kubectl get events --field-selector reason=FailedScheduling

```

## Cleanup resources

```bash
kubectl delete pod nginx-pod
```

## Links

- https://kubernetes.io/docs/concepts/scheduling-eviction/assign-pod-node/#affinity-and-anti-affinity
- https://kubernetes.io/docs/concepts/scheduling-eviction/assign-pod-node/#nodeselector
- https://kubernetes.io/docs/concepts/scheduling-eviction/taint-and-toleration/
- https://kubernetes.io/docs/concepts/scheduling-eviction/
