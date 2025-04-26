## Question

Create a PersistentVolume (PV) and a PersistentVolumeClaim (PVC) using an existing storage class named gold-stc-cka to meet the following requirements:

- Create a Persistent Volume (PV)

  - Name the PV as gold-pv-cka .
  - Set the capacity to 50Mi .
  - Use the volume type hostpath with the path /opt/gold-stc-cka .
  - Assign the storage class as gold-stc-cka .
  - Ensure that the PV is created on node01 , where the /opt/gold-stc-cka directory already exists.
  - Apply a label to the PV with key tier and value white .
- Create a Persistent Volume Claim (PVC)

  - Name the PVC as gold-pvc-cka .
  - Request 30Mi of storage from the PV gold-pv-cka using the matchLabels criterion.
  - Use the gold-stc-cka storage class.
  - Set the access mode to ReadWriteMany .
 
## Step 1: Create PV

```
apiVersion: v1
kind: PersistentVolume
metadata:
  name: gold-pv-cka
  labels:
    tier: white
spec:
  capacity:
    storage: 50Mi
  hostPath:
    path: /opt/gold-stc-cka
  storageClassName: gold-stc-cka
  nodeAffinity:
    required:
      nodeSelectorTerms:
        - matchExpressions:
            - key: kubernetes.io/hostname
              operator: In
              values:
                -  node01
  accessModes:
    - ReadWriteMany
```

## Step 2: Create PVC

```
apiVersion: v1
kind: PersistentVolumeClaim
metadata:
  name: gold-pvc-cka
spec:
  resources:
    requests:
      storage: 30Mi
  selector:
    matchLabels:
      tier: white
  storageClassName: gold-stc-cka
  accessModes:
    - ReadWriteMany
```
