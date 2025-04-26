## Question

Create a storage class called green-stc  as per the properties given below:

 - Provisioner should be kubernetes.io/no-provisioner .

 - Volume binding mode should be WaitForFirstConsumer .

 - Volume expansion should be enabled .

## Step 1: Create the StorageClass Configuration File

```
apiVersion: storage.k8s.io/v1
kind: StorageClass
metadata:
  name: green-stc
provisioner: kubernetes.io/no-provisioner
volumeBindingMode: WaitForFirstConsumer
allowVolumeExpansion: true
```
##  Step 2: Apply the StorageClass Configuration

```
kubectl apply -f storageclass.yml
```
