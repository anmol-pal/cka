Kubelet gets instruction from kube-api and create pods which are scheduled by kube-scheduler.

If there were no kube-api server ?
Kubelet can be configured to read pod definition file from ```etc/kubernetes/manifests``` if pod dies , kubelet will restart it. 
If file is removed from this directory , pod will be deleted automatically.
 

** Only pods can be created this way , not deployments or replica-sets

This can be configured when starting kubelet.

```
--pod-manifest-path=/etc/Kubernetes/manifests
```

Another way is to use 

kubelet.service
```
--config=kubeconfig.yaml
```
and static pod path ```staticPodPath: /etc/kubernetes/manifests```

1. Check option pod manifest path, 
2. else look for config option
3. Once static pods are created , we can view them using docker ps command, kubectl wont work cause it works with kube-api server.

Kubelet can take in input for creating pods from different ways , 
1. Use static pod path
2. Use HTTP API endpoint, which is used by kubelet , HTTP request is sent via kube-api server
3. Api-server is aware of the static-pods created by kubelet


Static Pods vs Daemon Sets
| Static Pods | Daemon Sets |
| -------- | ------- |
| Created by Kubelet | Created by Kube-api Server |
| Deploy Control Plane as Static pods | Deploy Monitoring and logging agents on node |