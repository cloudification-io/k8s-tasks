# Task 5 - Storage

## Contents

- [Task 5 - Storage](#task-5---storage)
  - [Contents](#contents)
  - [Assignment](#assignment)
  - [Example commands](#example-commands)
  - [Cleanup resources](#cleanup-resources)
  - [Links](#links)

## Assignment

1. Check available storage classses
2. Create PV and PVC
3. Create Pod that uses PVC
4. Exec into Pod and write some data into PVC
5. Delete Pod
6. Create new Pod using PVC. Read from PVC

## Example commands

Check StorageClassses

```bash
kubectl get storageclass
kubectl get sc

# Get detailed information about storage classes
kubectl describe storageclass
```

Create PV

```bash
# Create PV using YAML manifest
kubectl apply -f - <<EOF
apiVersion: v1
kind: PersistentVolume
metadata:
  name: my-pv
spec:
  capacity:
    storage: 1Gi
  accessModes:
    - ReadWriteOnce
  persistentVolumeReclaimPolicy: Retain
  storageClassName: default
  hostPath:
    path: /tmp/pv-data
EOF
```

Create PVC

```bash
# Create PVC using YAML manifest
kubectl apply -f - <<EOF
apiVersion: v1
kind: PersistentVolumeClaim
metadata:
  name: my-pvc
spec:
  accessModes:
    - ReadWriteOnce
  resources:
    requests:
      storage: 1Gi
  storageClassName: default
EOF
```

Create Pod with PVC mount

```bash
# Create Pod with PVC mounted
kubectl apply -f - <<EOF
apiVersion: v1
kind: Pod
metadata:
  name: storage-pod-1
spec:
  containers:
  - name: nginx
    image: nginx
    volumeMounts:
    - name: storage-volume
      mountPath: /data
  volumes:
  - name: storage-volume
    persistentVolumeClaim:
      claimName: my-pvc
EOF
```

Check that Pod is created and PVC status

```bash
❯ kg pod
NAME            READY   STATUS    RESTARTS   AGE
storage-pod-1   1/1     Running   0          4m33s

❯ kg pv
NAME    CAPACITY   ACCESS MODES   RECLAIM POLICY   STATUS   CLAIM            STORAGECLASS   VOLUMEATTRIBUTESCLASS   REASON   AGE
my-pv   1Gi        RWO            Retain           Bound    default/my-pvc   default        <unset>                          5m4s

❯ kg pvc
NAME     STATUS   VOLUME   CAPACITY   ACCESS MODES   STORAGECLASS   VOLUMEATTRIBUTESCLASS   AGE
my-pvc   Bound    my-pv    1Gi        RWO            default        <unset>                 4m59s
```

Exec into Pod and explore what is mounted

```bash
kubectl exec -it storage-pod-1 -- /bin/bash
```

Explore mounts

```bash
root@storage-pod-1:/# df -h
Filesystem      Size  Used Avail Use% Mounted on
overlay          39G  3.6G   34G  10% /
tmpfs            64M     0   64M   0% /dev
tmpfs           2.0G     0  2.0G   0% /data
```

Write something into mounted folder

```bash
echo "Hello from Pod 1!" > /data/message.txt
echo "Timestamp: $(date)" >> /data/message.txt
ls -la /data/
cat /data/message.txt
exit
```

Delete Pods and wait for Pod to be deleted

```bash
# Delete the first pod
kubectl delete pod storage-pod-1

# Verify pod is deleted
kubectl get pods
```

Create anoter Pod and read from volume

```bash
# Create a second pod using the same PVC
kubectl apply -f - <<EOF
apiVersion: v1
kind: Pod
metadata:
  name: storage-pod-2
spec:
  containers:
  - name: busybox
    image: busybox
    command: ['sleep', '3600']
    volumeMounts:
    - name: storage-volume
      mountPath: /data
  volumes:
  - name: storage-volume
    persistentVolumeClaim:
      claimName: my-pvc
EOF
```

Exec into 2nd Pod and explore mounted Volume

```bash
# Exec into the new pod and read the data
kubectl exec -it storage-pod-2 -- /bin/sh
```

## Cleanup resources

```bash
kubectl delete pod storage-pod-1 storage-pod-2 --ignore-not-found

kubectl delete pvc my-pvc

kubectl delete pv my-pv
```

## Links

- https://kubernetes.io/docs/concepts/storage/persistent-volumes/
- https://kubernetes.io/docs/concepts/storage/storage-classes/
- https://kubernetes.io/docs/concepts/storage/persistent-volumes/#persistentvolumeclaims
- https://kubernetes.io/docs/tasks/configure-pod-container/configure-persistent-volume-storage/
