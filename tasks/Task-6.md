# Task 6 - Deployment rollouts

## Contents

- [Task 6 - Deployment rollouts](#task-6---deployment-rollouts)
  - [Contents](#contents)
  - [Assignment](#assignment)
  - [Example commands](#example-commands)
  - [Cleanup resources](#cleanup-resources)
  - [Links](#links)

## Assignment

1. Create Nginx deployment
2. Verify Deployment
3. Patch deployment with new image version
4. Observe rollout
5. Do a rollback

## Example commands

Launch Deployment with specific image

```bash
kubectl create deployment nginx-rollout --image=nginx:1.21 --replicas=3
```

Verify Deployment is running

```bash
kubectl get deploy
```

Patch Deployment with new Image

```bash
kubectl set image deployment/nginx-rollout nginx=nginx:1.22
```

Watch new Pods

```bash
# Watch pods being updated in real-time
kubectl get pods -l app=nginx-rollout -w
```

Check rollout status

```bash
# Watch the rollout status
kubectl rollout status deployment/nginx-rollout
```

Check history

```bash
# Check rollout history
kubectl rollout history deployment/nginx-rollout
```

You can also use describe

```bash
# Get detailed rollout status
kubectl describe deployment nginx-rollout
```

Do a rollback

```bash
kubectl rollout undo deployment/nginx-rollout
```

Another option is to specify exact revision (if there was more than 1 update)

```bash
kubectl rollout undo deployment/nginx-rollout --to-revision=1
```

## Cleanup resources

```bash
kubectl delete deployment nginx-rollout

kubectl delete service nginx-rollout --ignore-not-found

kubectl delete pod test-pod --ignore-not-found
```

## Links

- https://kubernetes.io/docs/concepts/workloads/controllers/deployment/
- https://kubernetes.io/docs/tutorials/kubernetes-basics/update/update-intro/
- https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#rollout
- https://kubernetes.io/docs/concepts/workloads/controllers/deployment/#strategy
- https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#set
