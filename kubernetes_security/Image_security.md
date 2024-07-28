# Image security

* How to configure your pod to use image from a secure/private repository

```
kubectl create secret docker-registry regcred\
--docker-server= **** \
--docker-username= **** \
--docker-password= **** \
--docker-email= ****
```

and put this secret in pod definition file
```
spec:
    containers:
    - name: nginx
    imagepullSecrets:
    - name: regcred

```