# Task 4 - Service with LoadBalancer IP

## Contents

- [Task 4 - Service with LoadBalancer IP](#task-4---service-with-loadbalancer-ip)
  - [Contents](#contents)
  - [Assignment](#assignment)
  - [Example commands](#example-commands)
  - [Cleanup resources](#cleanup-resources)
  - [Links](#links)

## Assignment

1. Create Nginx Deployment
2. Expose Service with type:LoadBalancer
3. Use curl from laptop to reach LB IP

## Example commands

Crete Nginx deployment just like in previous task

Create Service for Nginx Deployment

```bash
kubectl expose deployment nginx-deployment --port=80 --target-port=80 --type=LoadBalancer
```

Check Service just like in previous task

Wait for Service to be assinged an External IP

```bash
kubectl get svc nginx-lb-deployment -w

...
NAME                  TYPE           CLUSTER-IP      EXTERNAL-IP     PORT(S)        AGE
nginx-lb-deployment   LoadBalancer   10.250.89.234   <EXTRERNAL_IP>   80:30723/TCP   70s
```

Check that Service is working

```bash
curl <EXTRERNAL_IP>
```

## Cleanup resources

```bash
kubectl delete service nginx-lb-deployment

kubectl delete deployment nginx-lb-deployment
```

## Links

- https://kubernetes.io/docs/concepts/services-networking/service/#loadbalancer
- https://kubernetes.io/docs/concepts/services-networking/service/#publishing-services-service-types
