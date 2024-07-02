## Limit Range

By default K8s does not have resources and limit configured so to enforce some limit use ```LimitRange```

```
apiVersion: v1
kind: LimitRange
metadata: 
    name: cpu-resource-constraint
spec:
    limits:
    - default:
        cpu: 500m
      defaultRequest:
        cpu: 500m
      max:
        cpu: "1"
      min:
        cpu: 100m
      type: Container       
```

LimitRange is available at NameSpace Level.
If these limits are changed , new-er pods are affected, not existing pods


If we want to restrict the total amount of resources that can be consumed at K8s cluster level 

## Resource Quota
```
apiVersion: v1
kind: ResourceQuota
metadata: 
    name: my-res-quota
spec:
    hard:
        requests.cpu: 4
        requests.memory: 4Gi
        limits.cpu: 10
        limits.memory: 10Gi
```