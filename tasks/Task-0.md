# Task 0 - Gain access to Namespaces

## Contents

- [Task 0 - Gain access to Namespaces](#task-0---gain-access-to-namespaces)
  - [Contents](#contents)
  - [Assignment](#assignment)
  - [Example commands](#example-commands)
  - [Cleanup resources](#cleanup-resources)
  - [Links](#links)

## Assignment

1. Download Kubeconfig (sent by email)
2. Place it in correct location or use ENV variable
3. Get list of namespaces
4. Set current context to correct namespace (with username)

## Example commands

Copy Kubeconfig to its default location

```bash
# Create .kube directory if it doesn't exist
mkdir -p ~/.kube

# Copy the downloaded kubeconfig to default location
cp ~/Downloads/kubeconfig-username.yaml ~/.kube/config

# Secure the file permissions
chmod 600 ~/.kube/config
```

Another option is to use ENV (useful with multiple configs)

```bash
export KUBECONFIG=~/Downloads/kubeconfig-username.yaml
```

Check list of avialable namespaces

```bash
# List all namespaces
kubectl get namespaces

# List namespaces with more details
kubectl get ns -o wide

# Show namespaces with labels
kubectl get namespaces --show-labels

# Describe a specific namespace
kubectl describe namespace default
```

Modify your kubeconfig and change default namespace

```bash
kubectl config get-contexts
```

Update default namespace

```bash
# Set context to use specific namespace (replace with actual values)
kubectl config set-context --current --namespace=<USERNAME_NAMESPACE>
```

Verify default namespace is updated by checking priviledges

(Check kubeconfig settings)

```bash
kubectl config get-contexts
```

(Verify access to resources in cluster)

```bash
kubectl auth can-i get pods
kubectl auth can-i create pods

## Extra
kubectl auth can-i --list
```

## Cleanup resources

```bash
kubectl delete pod nginx-pod
```

## Links

- https://kubernetes.io/docs/concepts/configuration/organize-cluster-access-kubeconfig/
- https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#config
- https://kubernetes.io/docs/concepts/overview/working-with-objects/namespaces/
- https://kubernetes.io/docs/reference/access-authn-authz/authorization/#checking-api-access
- https://kubernetes.io/docs/reference/kubectl/quick-reference/#kubectl-context-and-configuration
