Namespaced Resources:
- Pods
- Replicasets
- Jobs
- Deployments
- Services
- Secrets
- Roles
- Rolebinding
- ConfigMap
- PVC

Cluster Scope:
- Nodes
- PV
- ClusterRoles
- ClusterRoleBindings
- CertificateSigningRequests
- NameSpaces

examples of cluster roles
- Cluster Admin
    - view nodes
    - create nodes
    - delete nodes
- Storage Admin
    - view PVs
    - create PVs
    - delete PVs

```
apiVersion: rbac.authorization.k8s.io/v1
kind: ClusterRole
metadata: 
    name: cluster-administrator
rules:
- apiGroups: [""]
  resources: ["nodes"]
  verbs: ["list", "get", "create", "delete"]
```


Now link user to this role by creating a role binding

```
apiVersion: rbac.authorization.k8s.io/v1
kind: ClusterRoleBinding
metadata:
    name: cluster-admin-role-binding
subjects:
- kind: User
  name: cluster-admin
  apiGroup: rbac.authorization.k8s.io
roleRef:
  kind: ClusterRole
  name: cluster-administratir
  apiGroup: rbac.authorization.k8s.io
```

You can create ClusterRolbindings for a user even a namespaced resource , they ll have access to that resources across all namespaces