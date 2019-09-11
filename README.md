# Micro-paas
A Platform-as-a-service for testing application with a microservice architecture, using vagrant for building a network of virtual machine inside of which runs kubernetes.

This configuration will create the following virtual machines:
* A kubernetes master node  
* 2 kubernetes nodes
* A docker registry node

>The number of nodes can be changed by modifying the **N** variable inside the vagrant file.

### Prerequisites
For debian
```
sudo apt update
sudo apt install virtualbox vagrant ansible
vagrant plugin install vagrant-vbguest
```

For arch 
```
sudo pacman -Syu
sudo pacman -S virtualbox vagrant ansible
vagrant plugin install vagrant-vbguest
```

### Running the virtual environment
```
vagrant up
```

### Connect to the virtual machines
```
vagrant ssh k8s-master
vagrant ssh node-1
vagrant ssh node-2
vagrant ssh resgistry
```

### Examples
```
# On master node
$ kubectl get nodes
NAME         STATUS   ROLES    AGE    VERSION
k8s-master   Ready    master   106m   v1.15.3
node-1       Ready    <none>   100m   v1.15.3
node-2       Ready    <none>   95m    v1.15.3

$ kubectl get pods -A
NAMESPACE        NAME                                       READY   STATUS    RESTARTS   AGE
kube-system      calico-kube-controllers-65b8787765-7t765   1/1     Running   1          109m
kube-system      calico-node-b2qg2                          1/1     Running   1          109m
kube-system      calico-node-m69j8                          1/1     Running   1          104m
kube-system      calico-node-sxl5k                          1/1     Running   1          98m
kube-system      coredns-5c98db65d4-sm8wp                   1/1     Running   1          109m
kube-system      coredns-5c98db65d4-vb9jl                   1/1     Running   1          109m
kube-system      etcd-k8s-master                            1/1     Running   1          109m
kube-system      kube-apiserver-k8s-master                  1/1     Running   1          109m
kube-system      kube-controller-manager-k8s-master         1/1     Running   3          109m
kube-system      kube-proxy-7zjkn                           1/1     Running   1          109m
kube-system      kube-proxy-kzl52                           1/1     Running   1          104m
kube-system      kube-proxy-w9npr                           1/1     Running   1          98m
kube-system      kube-scheduler-k8s-master                  1/1     Running   3          109m
kube-system      kubernetes-dashboard-6b8c96cf8c-wgr7f      1/1     Running   1          109m
metallb-system   controller-6d6b8fcdb8-6n6j7                1/1     Running   1          109m
metallb-system   speaker-5xcwb                              1/1     Running   1          102m
metallb-system   speaker-d9l48                              1/1     Running   1          97m

$ kubectl get deployments
NAMESPACE        NAME                      READY   UP-TO-DATE   AVAILABLE   AGE
kube-system      calico-kube-controllers   1/1     1            1           114m
kube-system      coredns                   2/2     2            2           115m
kube-system      kubernetes-dashboard      1/1     1            1           114m
metallb-system   controller                1/1     1            1           114m

$ kubectl get services -A
NAMESPACE     NAME                   TYPE           CLUSTER-IP     EXTERNAL-IP     PORT(S)                  AGE
default       kubernetes             ClusterIP      10.96.0.1      <none>          443/TCP                  123m
kube-system   kube-dns               ClusterIP      10.96.0.10     <none>          53/UDP,53/TCP,9153/TCP   123m
kube-system   kubernetes-dashboard   LoadBalancer   10.98.72.161   192.168.1.240   8443:30339/TCP           27s

```

### Access to the dashboard
The dashboard address can be accessed here https://192.168.50.240 

