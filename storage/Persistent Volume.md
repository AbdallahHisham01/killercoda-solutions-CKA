## Question

Create a PersistentVolume (PV) named black-pv-cka with the following specifications:

 - Volume Type: hostPath
 - Path: /opt/black-pv-cka
 - Capacity: 50Mi

## Step 1: Create PV

```
apiVersion: v1
kind: PersistentVolume
metadata:
  name: black-pv-cka
spec:
  capacity:
    storage: 50Mi
  hostPath:
    path: /opt/black-pv-cka
  accessModes:
    - ReadWriteOnce            
```
