## Questions

There is existing Namespace applications .

- User smoke should be allowed to create and delete Pods, Deployments and StatefulSets in Namespace applications.
  
- User smoke should have view permissions (like the permissions of the default ClusterRole named view ) in all Namespaces but not in kube-system .
  
- Verify everything using kubectl auth can-i .

## Part 1
---

## Step 1: Create Role

```
kubectl create role smoke-role --verb=create,delete --resource=pods,deployments,statefulsets
```

## Step 2: Create RoleBinding

```
kubectl create rolebinding rolebinding-smoke --role smoke-role --user smoke -n applications
```

## Part 2
---

## Step 1:

```
kubectl create rolebinding smoke-rolebinding --clusterrole=view --user=smoke -n applications

kubectl create rolebinding smoke-rolebinding --clusterrole=view --user=smoke -n default

kubectl create rolebinding smoke-rolebinding --clusterrole=view --user=smoke -n kube-public

kubectl create rolebinding smoke-rolebinding --clusterrole=view --user=smoke -n kube-node-lease
```

## Verify:

```
kubectl auth can-i create deployments --as smoke -n applications # YES

kubectl auth can-i delete deployments --as smoke -n applications # YES

kubectl auth can-i delete pods --as smoke -n applications # YES

kubectl auth can-i delete sts --as smoke -n applications # YES

kubectl auth can-i list pods --as smoke -n default # YES
kubectl auth can-i list pods --as smoke -n applications # YES
kubectl auth can-i list pods --as smoke -n kube-public # YES
kubectl auth can-i list pods --as smoke -n kube-node-lease # YES
kubectl auth can-i list pods --as smoke -n kube-system # NO
```
  
