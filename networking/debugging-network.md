# CORE DNS

In large scale Kubernetes clusters , CoreDNS's memory usage is affected by number of pods and services.

K8s resources for core-dns are
1. service-account core-dns
2. cluster-roles coredns and kube-dns
3. clusterrolebinding coredns and kubedns
4. deployment coredns
5. config-map coredns
6. kube-dns service

Debugging tips
1. if core-dns is pending - check cni
2. if crashloopback on core dns pods -
    * Docker version of docker and node is running SE Linux
        a. upgrade new version of Docker
        b. disable SE Linux
        c. Modify the coredns deployment to set allowPrivilegeEscalation to true:
        ```
        kubectl -n kube-system get deployment coredns -o yaml | \ sed 's/allowPrivilegeEscalation: false/allowPrivilegeEscalation: true/g' | \ kubectl apply -f -
        ```
        d. Another cause for CoreDNS to have CrashLoopBackOff is when a CoreDNS Pod deployed in Kubernetes detects a loop.

            d.1 Add following to your kubelet config.yaml _resolvConf: this flag tells kubelet to pass alternate resolve.conf to pods. 

            disbale local DNS Cache on hostnode and restore /etc/resolve.conf

            Edit Corefile , replace /etc/resolv.conf with upstream DNS 8.8.8.8
            It only fixes coredns , kubelet will continue to use resolv.conf




        when analysing the coreDNS ```Corefile plugin``` defined in configmap
        Port 53 is used for DNS Resolution.
        ```
        kubernetes cluster.local in-addr.arpa ip6.arpa{
            pods insecure
            fallthrough in-addr.arpa ip6.arpa
            ttl 30
        }
        ```

        This is the backend to k8s for cluster local and reverse domains
        
        ```proxy . /etc/resolve.conf```

3. if CoreDNS and kube-dns are working fine , check kube-dns has valid endpoints.
    ```kubectl -n kube-system get ep kube-dns```
    if no endpoints for that service , inspect service and make sure it uses correct selector and ports


# Kube-Proxy

kube-proxy is a network proxy that runs on each node. It maintains network rules on node.

kubeproxy is responsible for watching services and endpoint associated with each service. 


run ```kubectl describe ds kube-proxy -n kube-system``` you can see that kube-proxy binary runs with following command inside kube-proxy

```
/usr/local/bin/kube-proxy
--config=/var/lib/kube-proxy/config.conf
--hostname-override=$(NODE\_NAME)
```

Debugging
1. check kube-proxy logs
2. check kube-proxy config map
3. check kube-proxy is running inside container
```
/var/folders/34/g1b6cj7x3yv89_57lsmrx0_w0000gn/T/com.apple.useractivityd/shared-pasteboard/items/64201050-E674-4BB6-918F-149858ABD53D/b04cd38597e01b12ed751ce2178aebfa450c2dcd.rtfd
```