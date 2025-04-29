## Question

There are existing Namespaces ns1 and ns2 .

Create ServiceAccount pipeline in both Namespaces.

These SAs should be allowed to view almost everything in the whole cluster. You can use the default ClusterRole view for this.

These SAs should be allowed to create and delete Deployments in their Namespace.

Verify everything using kubectl auth can-i .

## Solution

```
k create clusterrolebinding --clusterrole=view --serviceaccount=ns1:pipeline crb1

k create clusterrolebinding --clusterrole=view --serviceaccount=ns2:pipeline crb2

k create role -n ns1 --resource=deployments --verb=create,delete role1

k create rolebinding -n ns1 --role=role1 --serviceaccount=ns1:pipeline  rb1

k create role -n ns2 --verb=create,delete --resource=deployments r2

k create rolebinding -n ns2 rb2 --role=r2 --serviceaccount=ns2:pipeline
```
