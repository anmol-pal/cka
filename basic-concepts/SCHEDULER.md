# Kube scheduler 
Decides which pod is scheduled on which node , but pod is created via kubelet

How does scheduler identify which node is best to place the pod on
* Filter via nodes not having enough CPU
* Scheduler then ranks the nodes based on a priority function

```cat /etc/kubernetes/manifests/kube-scheduler.yaml```