## Question
A persistent volume named red-pv-cka is available. Your task is to create a PersistentVolumeClaim (PVC) named red-pvc-cka and request 30Mi of storage from the red-pv-cka PersistentVolume (PV).

Ensure the following criteria are met:

 - Access mode: ReadWriteOnce
 - Storage class: manual

## Step 1: Create PVC

```
apiVersion: v1
kind: PersistentVolumeClaim
metadata:
  name: red-pvc-cka
spec:
  resources:
    requests:
      storage: 30Mi
  accessModes:
    - ReadWriteOnce
  storageClassName: manual
  volumeName: red-pv-cka
```
