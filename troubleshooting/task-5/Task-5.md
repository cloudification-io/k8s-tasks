# Task 5 - 

## Contents

- [Task 5 -](#task-5--)
  - [Contents](#contents)
  - [Assignment](#assignment)
  - [Example commands](#example-commands)
  - [Cleanup resources](#cleanup-resources)
  - [Links](#links)

## Assignment

1. Apply with kubectl
2. Investigate why StatefulSet is not working

## Example commands

Apply objects via kubectl

```bash
kubectl apply -f deployment.yml
```

Useful debug commands

```bash
kubectl get events

kubectl get pods

kubectl describe pod

kubectl describe statefulset
```

## Cleanup resources

```bash
kubectl delete pod nginx-pod
```

## Links

- https://kubernetes.io/docs/concepts/workloads/controllers/statefulset/
- https://kubernetes.io/docs/concepts/configuration/manage-resources-containers/
- https://kubernetes.io/docs/concepts/scheduling-eviction/
- https://kubernetes.io/docs/concepts/policy/resource-quotas/
- https://kubernetes.io/docs/tasks/debug/debug-application/
