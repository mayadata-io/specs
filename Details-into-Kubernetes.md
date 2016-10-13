## Tips to Kubernetes from Scratch

- Refer [scratch](http://kubernetes.io/docs/getting-started-guides/scratch/)

<br />

### Cloud Provider 
- Specs - pkg/cloudprovider/cloud.go
- Manages load balancers, nodes, & networking routes

<br />

### On IPs

- Need to provide a block of IPs to Kubernetes to be used as PODs IPs
- Pod to pod communication via IP of the pod 
  - overlay network 
    - via traffic encapsulation
  - without overlay  
    - Configure switches, routers to be aware of POD IPs
    - Better performance
- Supports CNI network plugin interface
- IPv6 is not supported for POD IPs
  - e.g. use 10.10.0.0/16 as the range for the cluster, 
    - with up to 256 nodes using 10.10.0.0/24 through 10.10.255.0/24, respectively.
  - e.g. A /24 per node supports 254 pods per machine and is a common choice. 
    - If IPs are scarce, a /26 (62 pods per machine) or even a /27 (30 pods) may be sufficient.
- Kubernetes allocates an IP to each service.
  - However these IPs need not be routable
  - kube-proxy takes care of translating Service IPs to POD IPs before traffic leaves the node
  - Need to allocate a block of IPs for the services 
    - e.g. SERVICE_CLUSTER_IP_RANGE = "10.0.0.0/16" means 65534 services can be active simultaneously
- Pick up a static IP for master node
  - e.g. **MASTER_IP**
- Open access to apiserver ports 80 &/or 443
 - Enable ipv4 forwarding: sysctl net.ipv4.ip_forward = 1
- Can have fine grained networking policy between PODs using Network Policy resource

<br />

### Regions

- Clusters can be represented as regions
  - Provide a cluster name e.g. **CLUSTER_NAME**

<br />

### Binaries

- The Kubernetes binaries required are:
  - etcd, docker/rkt, kubelet, kube-proxy, kube-apiserver, kube-controller-manager, kube-scheduler
  - https://github.com/kubernetes/kubernetes/releases/latest
  - Kubernetes binary has all its dependant binaries
- What should run outside the container ?
  - *docker, kubelet, kube-proxy* ~ same way as we run the system daemons
  - Hence bare binaries are reqd
- What should run as-a container ?
  - *etcd, kube-apiserver, kube-controller-manager, & kube-scheduler*
  - Hence images are required
  - Get the images from gcr.io/google_containers/hyperkube:$TAG
- Building images is also possible
  - Release contain files s.a ./kubernetes/server/bin/kube-apiserver.tar
  - Convert above file to an image *docker load -i kube-apiserver.tar*
  - Similarly for etcd *cd kubernetes/cluster/images/etcd; make*
  - NOTE: **use the etcd version provided in the Kubernetes distribution**
  - Check the value of TAG in the *kubernetes/cluster/images/etcd/Makefile*
- Setting the env vars
  - HYPERKUBE_IMAGE=gcr.io/google_containers/hyperkube:$TAG
  - ETCD_IMAGE=gcr.io/google_containers/etcd:$ETCD_VERSION
- Verify the image & tag
  - *docker images*
- NOTE - hyperkube is a all-in-one binary
  - hyperkube kubelet runs kubelet
  - hyperkube apiserver runs apiserver

### HTTPS access to apiserver

- refer [creating certificates](http://kubernetes.io/docs/admin/authentication/#creating-certificates)
- Need to prepare the certs & credentials
- Master needs a cert to act as an HTTPS server
- kubelets optionally need certs
  - to identify themselves as clients of the master
  - & also while serving its API over HTTPS
- Generate a root cert
  - use this to sign the master, kublet & kubectl certs
- Files
  - CA_CERT is put at apiserver node @ */srv/kubernetes/ca.crt*
  - MASTER_CERT signed by CA_CERT & put at apiserver node @ */srv/kubernetes/server.crt*
  - MASTER_KEY put at apiserver node @ */srv/kubernetes/server.key*
  - KUBELET_CERT *optional*
  - KUBELET_KEY *optional*


### Credentials

- Admin needs token or password to get identified
  - tokens are alphanumeric e.g. 32 chars
- Tokens need to be stored in a file for the apiserver to read
  - */var/lib/kube-apiserver/known_tokens.csv*
- How to distribute credentials to clients ?
  - Put them into a **kubeconfig** file
  - refer [kubeconfig](http://kubernetes.io/docs/user-guide/kubeconfig-file/)
  - Use kubectl commandline options

### kubconfig file for administrators

```bash

# non-https option
kubectl config set-cluster $CLUSTER_NAME --server=http://$MASTER_IP --insecure-skip-tls-verify=true

# https option
kubectl config set-cluster $CLUSTER_NAME --certificate-authority=$CA_CERT --embed-certs=true --server=https://$MASTER_IP

# Set the default cluster to use
kubectl config set-context $CONTEXT_NAME --cluster=$CLUSTER_NAME --user=$USER
kubectl config use-context $CONTEXT_NAME
```

### kubeconfig file for others

- What are others here ?
  - kubelet & kube-proxy
- There are 3 possible options
  - same credentials as the admin
  - one token & kubeconfig file for all kubelets, one for all kube-proxy & one for admin
  - different credentials for every kubelet, etc
- How to do it ?
  - copy $HOME/.kube/config
  - or learn the code @ cluster/gce/configure-vm.sh
  - or a template
  - to dest @ 
    - /var/lib/kube-proxy/kubeconfig
    - /var/lib/kubelet/kubeconfig

### Configuring Base Software on Nodes

- Base OS + docker + kubelet + kube-proxy
- Docker version depends on kubelet version
- Need to install docker with Kubernetes specific options
  - else remove the networking settings

```bash
iptables -t nat -F
ip link set docker0 down
ip link delete docker0
```

### Docker networking as per Kubernetes

- Create own bridge for the per-node CIDR ranges
  - set --bridge=cbr0
- Docker should not manage iptables for host-ports & instead let kube-proxy do this
  - set --iptables=false
- If we want POD IP to be routable
  - set --ip-masq=false
- If using flannel, need to consider the extra packet size due to udp encapsulation
  - set --mtu=
- If you want to connect to a private registry without using SSL
  - --insecure-registry $CLUSTER_SUBNET
- Perhaps need to increase the no. of open files for docker
  - DOCKER_NOFILE=1000000
- NOTE: *Ensire docker works correctly before proceeding with rest of install*

