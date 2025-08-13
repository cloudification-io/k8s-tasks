# Task 7 - Observing logs

## Contents

- [Task 7 - Observing logs](#task-7---observing-logs)
  - [Contents](#contents)
  - [Assignment](#assignment)
  - [Example commands](#example-commands)
  - [Cleanup resources](#cleanup-resources)
  - [Links](#links)

## Assignment

1. 1. Create Job with PVC mount
2. Do a simple loop to write date to file and exit after 10 seconds
3. Watch for Job to complete
4. Check PVC is available
5. Create Pod that uses this PVC and tails its contents
6. Check logs of the running Pod

## Example commands

Create PVC and a Job that writes into this volume

```bash
# Create PVC for the job
kubectl apply -f - <<EOF
apiVersion: v1
kind: PersistentVolumeClaim
metadata:
  name: job-pvc
spec:
  accessModes:
    - ReadWriteOnce
  resources:
    requests:
      storage: 1Gi
EOF

# Create Job with PVC mount
kubectl apply -f - <<EOF
apiVersion: batch/v1
kind: Job
metadata:
  name: date-writer-job
spec:
  template:
    spec:
      containers:
      - name: date-writer
        image: busybox
        command: ["/bin/sh"]
        args:
        - -c
        - |
          echo "Starting date writer job..."
          for i in 1 2 3 4 5 6 7 8 9 10; do
            echo "$(date): Iteration $i" >> /data/dates.log
            sleep 1
          done
          echo "Job completed at $(date)" >> /data/dates.log
          echo "Job finished successfully"
        volumeMounts:
        - name: job-storage
          mountPath: /data
      volumes:
      - name: job-storage
        persistentVolumeClaim:
          claimName: job-pvc
      restartPolicy: Never
  backoffLimit: 3
EOF
```

Observer Job running

```bash
kubectl get jobs -w
```

Optionally check logs of a job Pod

```bash
kubectl logs -l job-name=date-writer-job -f
```

Create another Pod that uses same PVC and checks its contents

```bash
# Create Pod that mounts the PVC and tails the file
kubectl apply -f - <<EOF
apiVersion: v1
kind: Pod
metadata:
  name: log-reader-pod
spec:
  containers:
  - name: log-reader
    image: busybox
    command: ["/bin/sh"]
    args:
    - -c
    - |
      echo "Starting log reader..."
      echo "Contents of /data:"
      ls -la /data/
      echo "Reading dates.log file:"
      if [ -f /data/dates.log ]; then
        cat /data/dates.log
        echo "Tailing the file (press Ctrl+C to stop):"
        tail -f /data/dates.log
      else
        echo "dates.log file not found!"
        sleep 3600
      fi
    volumeMounts:
    - name: job-storage
      mountPath: /data
  volumes:
  - name: job-storage
    persistentVolumeClaim:
      claimName: job-pvc
  restartPolicy: Never
EOF
```

Check logs of reader Pod

```bash
kubectl logs log-reader-pod
```

Optionally follow logs in real time

```bash
kubectl logs -f log-reader-pod
```

## Cleanup resources

```bash
kubectl delete pod log-reader-pod

kubectl delete job date-writer-job

kubectl delete pvc job-pvc
```

## Links

- https://kubernetes.io/docs/concepts/workloads/controllers/job/
- https://kubernetes.io/docs/concepts/workloads/controllers/job/#running-an-example-job
- https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#wait
- https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#logs
