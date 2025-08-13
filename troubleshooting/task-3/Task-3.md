# Task 0 - 

## Contents

- [Task 0 -](#task-0--)
  - [Contents](#contents)
  - [Assignment](#assignment)
  - [Example commands](#example-commands)
  - [Cleanup resources](#cleanup-resources)
  - [Links](#links)

## Assignment

1. Download Kubeconfig (sent by email)

## Example commands

Apply objects via Kustmomize

```bash
kustomize build . | kubectl apply -f -
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
kustomize build . | kubectl delete -f -
```

## Links

- https://kubernetes.io/docs/tasks/manage-kubernetes-objects/kustomization/
- https://kubernetes.io/docs/concepts/services-networking/service/
- https://kubernetes.io/docs/concepts/overview/working-with-objects/labels/
- https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#kustomize
