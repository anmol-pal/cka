k8s initially only supported docker initially but more container interfaces were coming in - 
K8s introduced CRI (Container Runtine Interface) - Any container runtime can be run using k8s as long as they follow (OCI) - Open Container Initiative standard
Docker was not built following OCI , for k8s to support docker k8s introduced Dockershim