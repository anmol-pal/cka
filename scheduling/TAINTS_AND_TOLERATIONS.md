Taints and Tolerations are restrictions on what can be scheduled on a nodes

## Taints

Consider example were a node <Node1> is dedicated to a certain application , you'd only like pods belonging to those apps be scheduled on this node.

You'd apply taint on this node , to make sure other pods are not. 
You'd apply toleration on the pod to make sure when its scheduled on this <Node1> is ok , any other pod without toleration can not be scheduled on this <Node1>

```kubectl taint nodes node-name key=value:taint-effect```

Also note , that its not guranteed that taint and toleration will ensure <Pod1> is scheduled at <Node1> , its possible <Pod1> can get scheduled at any other nodes. 

Taints will ensure only pods of a certain toleration are scheduled over it.

To make sure a pod is scheduled on a certain node use ```Affinity```


### Taint Effect [ NoSchedule | PreferNoSchedule | NoExecute ]

**NoSchedule** - Pod will not scheduled on node
**PreferNoSchedule** - System will try to avoid placing pod on the node , not guranteed
**NoExecute** - New pods won't be scheduled and existing pods which do not tolerate the taint will be evicted  
```kubectl taint node node1 app=blue:NoSchedule```


## Tolerations

Tolerartions are applied to pods - Should be in double quotes

```
apiVersion: v1
kind: Pod
metadata:
    name: myapp
spec:
    containers:
    - name: ngnix
      image: ngnix
    tolerations:
    - key: "app"
      operator: "Equal"
      value: "blue"
      effect: "NoSchedule"

```

Master Node: 
    Scheduler does not schedule any pod at master node, because a taint is set automatically to prevent any pods scheduling on master , can be configured otherwise too 
    ```
    kubectl describe node kubemaster | grep Taint
    Taint:   node-role.kubernetes.io/master:NoSchedule
    ```