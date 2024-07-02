# Kubelet
When a kubelet recieves instruction to run a pod , it requests container runtime engine to pull image and run
Kubelet then monitors state of pod and reports it to kube-api server

- Kubeadm does not deploy the kubelet automatically, you need to manually install the kubelet 