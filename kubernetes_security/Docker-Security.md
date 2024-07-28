root user in a container does not have same privileges as root on host.
Host has a namespace , and container has their own namespace.
Docker container runs in its own namespace and can not see anything outside.

If you do not want process inside container to be run as a root user, you may choose set user option , or have it defined at time of building image

```
docker run --user=1000 ubuntu sleep 3600
```

Dockerfile
```
FROM ubuntu
USER 1000
```

Now root user inside container won't be same as root on host.
These capabilities are ```/usr/include/linux.capability.h```

To provide additional privileges 
```
docker run --cap-add MAC_AD ubuntu

docker run --cap-add KILL ubuntu

docker run --privileged ubuntu # All permissions enabled
```

# Security in k8s pods

```
apiVersion: v1
kind: Pod
metadata:
    name: web-pod
spec:
    containers:
        - name: ubuntu
          image: ubuntu
          command: ["sleep", "3600"]
          securityContext:
            runAsUser: 1000
            capabilities:  #Only available at container level , not pod level
                add: ["MAC_ADMIN"]

```



