## Question

There exists a deployment named nginx-deployment exposed through a service called nginx-service . Create an ingress resource named nginx-ingress-resource to efficiently distribute incoming traffic with the following settings: pathType: Prefix , path: /shop , Backend Service Name: nginx-service , Backend Service Port: 80 , ssl-redirect should be configured as false .

## Solution

```
apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
  name: nginx-ingress-resource
  annotations:
    nginx.ingress.kubernetes.io/ssl-redirect: "false"
spec:
  rules:
    - http:
        paths:
          - pathType: Prefix
            path: /shop
            backend:
              service:
                name: nginx-service
                port:
                  number: 80
```
