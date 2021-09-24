# Material de apoyo módulo 2

[Presentación del Modulo 2](https://1drv.ms/p/s!AoX_zvfKf0RXj8l5P9etkYLRmJ4pdw?e=TWX49g "Presentación")

1. **Kubespray** https://kubernetes.io/docs/setup/production-environment/tools/kubespray/ 
2. **KOPS** https://kubernetes.io/docs/setup/production-environment/tools/kops/ 
3. **EKSCTL** https://eksctl.io/ 
4. **Kubecorn** http://kubicorn.io/ 
5. **Kubeadm** https://kubernetes.io/docs/setup/production-environment/tools/kubeadm/create-cluster-kubeadm/ 


## Instalació de Kubernetes: 

1. ```root@masteredteam:˜# apt-get update && apt-get upgrade -y```
2. ```root@masteredteam:˜# apt-get install -y vim```
3. ```root@masteredteam:˜# apt-get install -y docker.io```
4. ```root@masteredteam:˜# vim /etc/apt/sources.list.d/kubernetes.list
> deb http://apt.kubernetes.io/ kubernetes-xenial main
5. ```root@master:˜# curl -s https://packages.cloud.google.com/apt/doc/apt-key.gpg | apt-key add - ```
> OK
6. ```root@master:˜# apt-get update```
