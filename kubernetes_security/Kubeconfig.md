How would you query a kubernetes cluster for pods?

```
curl https://my-kube-cluster:6443/api/v1/pods \
    --key admin.key
    --cert admin.crt
    --cacert ca.crt

{
    kind: "PodList"
    "apiVersion": "v1"
    "metadata": {
        "selfLink": "/api/v1/pods",
    },
    "items": []
}
```
similar request made via kubectl
```
kubectl get pods
    --server my-kube-cluster
    --client-key admin.key
    --client-certificate admin.crt
    --certificate-authority ca.crt
```
Now all these options are moved to a kubeconfig file
default ```$HOME/.kube/config```

A kubeconfig 
1. Clusters - development, production
3. Users - admin / devuser / produser 
2. Contexts - admin@development , produser@production
 
```
apiVersion: v1
kind: Config

clusters:
- name: my-kube-cluster
  cluster: 
    certificate-authority: ca.crt
    server: https://my-kube-cluster:6443

contexts:
- name: my-kube-admin@my-kube-cluster
  context:


users:
- name: my-kube-admin
  user:
    client-certificate: admin.crt
    client-key: admin.key
```

How does kubectl select context? 
1. Specify default context
2. ```kubectl config view``` - to see which is current set context
3. ```kubectl config set-context my-kube-admin@my-kube-cluster```