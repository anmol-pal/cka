When an OS Upgrade is happening on a node , how to protect workloads?


1. Mark the node cordoned  such that it becomes unschedulable, no new nodes are scheduled on it
```
k cordon node01
```

2. Drain nodes , move workload to uncordoned nodes.
To get drained properly , a pod needs to be part of replica-set or daemon-set or  a deployment so that kubelet creates it again on an uncordoned node
```
k drain node01 --ignore-daemonsets
```

3. <OS Patch is going on rn>

4. Uncordon node again
```
k uncordon node01
```

