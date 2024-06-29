# Kube Proxy

A service is not an actively listening process or a container like pod , so no IP can be attached to it, now to make a service accessible across the nodes.

Kube-proxy  -
 This process runs on each node of a k8s cluster, it looks for all the new servcies being created , and for each new service an appropriate rule is created to forward traffic to those services to backend pods, using IP Table rules. 

