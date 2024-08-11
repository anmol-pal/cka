We have custom  cni script , which we pass to kubelet

```
--cni-conf-dir = /etc/cni/net.d
--cni-bin-dir = /etc/cni/bin

```
It deploys an agent on each node.
When a packet is sent from one node to another , agent intercepts the packet and checks  for destination.
Each agent / Peer stores topology of entire setup, this way agents have information about IPs on other nodes.
Weave creates its own bridge on nodes and names it ```weave```
It assigns IP address to each network.
A pod may be attached to multiple bridge networks , i.e. a pod can be attached to both [ weave bridge and docker bridge]
What path a packet takes to reach destination, depends on route configured on container.


# Deploying Weave

It can be deployed as services or daemons on each cluster as pods or manually.



