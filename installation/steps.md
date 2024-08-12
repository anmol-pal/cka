# Steps to install k8s cluster 1 master , 2 worker - using kubeadm

1. Installing kubeadm
    - Install a container runtime ```containerd``` in this case on all 3 hosts
    - make sure container runtime is using same cgroup driver as kubelet systemd.
        ```ps -p 1``` and restart containerd
    - Install kubeadm , kubelet, kubectl
    - initialising control plane 
    kubeadm init , --pod-network-cidr, --apiserver-advertise-address on master 
    check ```ip add``
    ```kubeadm init --pod-network-cidr=10.244.0.0/16 --apiserver-adverstise-address=<ip-add>```

    - mkdir -p $HOME/.kube.... output of previous command
    - Now deploy your pod network
    ```install weave net or any other cni```
    - Join your worker nodes - on worker nodes
    ```kubeadm join 192.168.56.2:6443 --token <sometoken output from previous command at master> --discovery-token-ca-cert-hash <output from previous command at master>```


Setting bridge

```
cat <<EOF | sudo tee /etc/modules-load.d/k8s.conf
br_netfilter
EOF

cat <<EOF | sudo tee /etc/sysctl.d/k8s.conf
net.bridge.bridge-nf-call-ip6tables = 1
net.bridge.bridge-nf-call-iptables = 1
EOF

sudo sysctl --system
```


```
sudo apt-get update

sudo apt-get install -y apt-transport-https ca-certificates curl

curl -fsSL https://pkgs.k8s.io/core:/stable:/v1.30/deb/Release.key | sudo gpg --dearmor -o /etc/apt/keyrings/kubernetes-apt-keyring.gpg

echo 'deb [signed-by=/etc/apt/keyrings/kubernetes-apt-keyring.gpg] https://pkgs.k8s.io/core:/stable:/v1.30/deb/ /' | sudo tee /etc/apt/sources.list.d/kubernetes.list

sudo apt-get update

# To see the new version labels
sudo apt-cache madison kubeadm

sudo apt-get install -y kubelet=1.30.0-1.1 kubeadm=1.30.0-1.1 kubectl=1.30.0-1.1

sudo apt-mark hold kubelet kubeadm kubectl
```