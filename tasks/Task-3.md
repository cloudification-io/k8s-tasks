# Task 3 - Deployment with Service

## Contents

- [Task 3 - Deployment with Service](#task-3---deployment-with-service)
  - [Contents](#contents)
  - [Assignment](#assignment)
  - [Example commands](#example-commands)
  - [Cleanup resources](#cleanup-resources)
  - [Links](#links)

## Assignment

1. Create Nginx deployment
2. Expose Service with ClusterIP
3. Port-forward Service and curl into it

## Example commands

Launch Pod

```bash
kubectl create deployment nginx-deployment --image=nginx --replicas=3
```

Launch Pod (via YAML)

```bash
kubectl apply -f - <<EOF
apiVersion: apps/v1
kind: Deployment
metadata:
  name: nginx-deployment
  labels:
    app: nginx
spec:
  replicas: 3
  selector:
    matchLabels:
      app: nginx
  template:
    metadata:
      labels:
        app: nginx
    spec:
      containers:
      - name: nginx
        image: nginx
        ports:
        - containerPort: 80
EOF```
```

Check Deployment

```bash
❯ kubectl get deploy
NAME               READY   UP-TO-DATE   AVAILABLE   AGE
nginx-deployment   3/3     3            3           27s
```

Expose Service for Nginx Deployment

```bash
kubectl expose deployment nginx-deployment --port=80 --target-port=80 --type=ClusterIP
```

Check Service

```bash
❯ kubectl get svc
NAME               TYPE        CLUSTER-IP       EXTERNAL-IP   PORT(S)   AGE
nginx-deployment   ClusterIP   100.64.146.184   <none>        80/TCP    18s
```

Check full Service YAML

```bash
❯ kubectl get svc nginx-deployment -o yaml
apiVersion: v1
kind: Service
metadata:
  labels:
    app: nginx-deployment
  name: nginx-deployment
...
```

Port-forward Service port to local port (format: <LOCAL_PORT>:<REMOTE_PORT>)

```bash
❯ kubectl port-forward svc/nginx-deployment 8080:80
Forwarding from 127.0.0.1:8080 -> 80
Forwarding from [::1]:8080 -> 80
```

Check connection

```bash
curl localhost:8080
```

## Cleanup resources

```bash
kubectl delete deployment nginx-deployment

kubectl delete service nginx-deployment
```

## Links

- https://kubernetes.io/docs/concepts/workloads/pods/
- https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#run
- https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#port-forward
