```yml
apiVersion: v1
kind: PersistentVolumeClaim
metadata:
  name: node-pvc
spec:
  accessModes:
    - ReadWriteOnce
  resources:
    requests:
      storage: 1Gi
```