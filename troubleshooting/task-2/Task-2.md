# Task 2 - Deployment failing 1

## Contents

- [Task 2 - Deployment failing 1](#task-2---deployment-failing-1)
  - [Contents](#contents)
  - [Assignment](#assignment)
  - [Example commands](#example-commands)
  - [Cleanup resources](#cleanup-resources)
  - [Links](#links)

## Assignment

1. Apply manifests via kubectl
2. Check why deployment is not working

## Example commands

Apply objects via kubectl

```bash
kubectl apply -f deployment.yml
```

Useful debug commands

```bash
kubectl get deploy
kubectl desribe deploy

kubectl get deploy <NAME> -o yaml
```

Fix errors

```bash
kubectl edit deploy <NAME>
```

## Cleanup resources

```bash
kubectl delete -f deployment.yml
```

## Links

- https://kubernetes.io/docs/concepts/configuration/organize-cluster-access-kubeconfig/
