# Setup basic authentication on kubernetes


## Not recommended

Create a file with users locally
`/tmp/users/user-details.csv`
Format <password><user-name><userid>
```
\# User file contents
password123,user1,u0001
password123,user2,u0002
password123,user3,u0003
```


Now edit kube-api server and pass user-details
* Mount volume such that this file is accessible inside container
* Add option of --basic-auth while startup
```
apiVersion: v1
kind: Pod
metadata:
    name: kube-apiserver
    namespace: kube-system
spec:
  containers:
  - command:
    - kube-apiserver
    - --autthorization-mode=Node,RBAC
    - --basic-auth-file=/tmp/users/user-details.csv

    image: k8s.gcr.io/kube-apiserver-amd64:v1.11.3
    name: kube-apiserver
    volumeMounts:
    - mountPath = /tmp/users
      name: usr-details
      readOnly: true
    volumes:
    - hostPath:
        path: /tmp/users
        type: DirectoryOrCreate
    name: usr-details
```


Now create RoleBindings 
```
kind: Role
apiVersion: rbac.authorization.k8s.io/v1
metadata:
    namespace: default
    name: pod-reader
rules:
- apiGroups: \[""\] # "" indicates core API Group
  resources: \["pods"\]
  verbs: \["get", "watch", "list"\]

```

```
kind: RoleBinding
apiVersion: rbac. authorization.k8s.io/v1
metadata:
    name: read-pods
    namespace: default
subjects:
- kind: User
  name: user1
  apiGroup: rbac.authorization.k8s.io
roleRef:
  kind: Role
  name: pod-reader #Must match the role you wish to bind with
  apiGroup: rbac.authorization.k8s.io
```

Once created , you may authenticate into kube-apiserver using users credentials

```curl -v -k https://localhost:6443/api/v1/pods -u "user:user1:password123"```
