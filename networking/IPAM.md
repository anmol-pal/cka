# IPAM - IP Address Management

Covers how are the virtual bridge networks and nodes are assigned IP Subnets
How are Pods assigned IP? and how is it ensured they are not duplicated?


- CNI Plugin is responsible for this.

When starting cni , we set the IP range  , and that is split equally among all nodes to be assigned to pods
