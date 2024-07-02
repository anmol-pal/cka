# Node Affinity

![alt text](image-1.png)

```
affinity:
    nodeAffinity:
        requiredDuringSchedulingIgnoredDuringExecution:
            nodeSelectorTerms:
            - matchExpressions:
                - key: size
                  operator: In / NotIn / Exists . . .
                  value: 
                   - Large
```

Different Node Affinities

requiredDuringScheduleIgnoredDuringExecution
preferredDuringScheduleIgnoredDuringExecution
![alt text](image-2.png)

requiredDuringScheduleRequiredDuringExecution
preferredDuringScheduleRequiredDuringExecution
![alt text](image-3.png)