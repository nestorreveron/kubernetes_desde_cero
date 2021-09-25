# Material de apoyo módulo 2

[Presentación del Modulo 2](https://1drv.ms/p/s!AoX_zvfKf0RXj8l5P9etkYLRmJ4pdw?e=TWX49g "Presentación")

1. **Kubespray** https://kubernetes.io/docs/setup/production-environment/tools/kubespray/ 
2. **KOPS** https://kubernetes.io/docs/setup/production-environment/tools/kops/ 
3. **EKSCTL** https://eksctl.io/ 
4. **Kubecorn** http://kubicorn.io/ 
5. **Kubeadm** https://kubernetes.io/docs/setup/production-environment/tools/kubeadm/create-cluster-kubeadm/ 


## Instalación de Kubernetes: 

1. ```root@masteredteam:˜# apt-get update && apt-get upgrade -y```
2. ```root@masteredteam:˜# apt-get install -y vim```
3. ```root@masteredteam:˜# apt-get install -y docker.io```
4. ```root@masteredteam:˜# vim /etc/apt/sources.list.d/kubernetes.list```
> *deb http://apt.kubernetes.io/ kubernetes-xenial main*
5. ```root@masteredteam:˜# curl -s https://packages.cloud.google.com/apt/doc/apt-key.gpg | apt-key add - ```
> *OK*
6. ```root@masteredteam:˜# apt-get update```
7. ```root@masteredteam:˜# apt-get install -y kubeadm=1.18.1-00 kubelet=1.18.1-00 kubectl=1.18.1-00```
8. ```root@masteredteam:˜# apt-mark hold kubelet kubeadm kubectl```
9. ```root@masteredteam:˜# wget https://docs.projectcalico.org/manifests/calico.yaml```
10. ```root@masteredteam:˜# less calico.yaml```
```
1 ....
2 # The default IPv4 pool to create on startup if none exists. Pod IPs will be
3 # chosen from this range. Changing this value after installation will have
4 # no effect. This should fall within `--cluster-cidr`.
5 - name: CALICO_IPV4POOL_CIDR
6 value: "192.168.0.0/16"
7 ....
```
11. ```root@masteredteam:˜# ip addr show```
12. ```root@masteredteam:˜# vim /etc/hosts```
> *10.128.0.3 k8smasteredteam #<-- Add this line*
> *127.0.0.1 localhost*
13. ```root@masteredteam:˜# vim kubeadm-config.yaml```
```
1 apiVersion: kubeadm.k8s.io/v1beta2
2 kind: ClusterConfiguration
3 kubernetesVersion: 1.18.1 #<-- Use the word stable for newest version
4 controlPlaneEndpoint: "k8smasteredteam:6443" #<-- Use the node alias not the IP
5 networking:
6 podSubnet: 192.168.0.0/16 #<-- Match the IP range from the Calico config file
```
14. ```root@masteredteam:˜# kubeadm init --config=kubeadm-config.yaml --upload-certs | tee kubeadm-init.out # Save output for future review```
15. ```root@masteredteam:˜# exit```
16. ```student**@masteredteam:˜$ mkdir -p $HOME/.kube```
17. ```student@masteredteam:˜$ sudo cp -i /etc/kubernetes/admin.conf $HOME/.kube/config``
18. ```student@masteredteam:˜$ sudo chown $(id -u):$(id -g) $HOME/.kube/config```
19. ```student@masteredteam:˜$ less .kube/config```
20. ```student@masteredteam:˜$ sudo cp /root/calico.yaml .```
21. ```student@masteredteam:˜$ kubectl apply -f calico.yaml```
22. ```student@masteredteam:˜$ sudo apt-get install bash-completion -y```
> exit and log back in
23. ```student@masteredteam:˜$ source <(kubectl completion bash)```
24. ```student@masteredteam:˜$ echo "source <(kubectl completion bash)" >> $HOME/.bashrc```
25. ```student@masteredteam:˜$ sudo kubeadm config print init-defaults```

## Configuración del Worker Node para hacer el Join al Master Node: 

1. ```student@workeredteam:˜$ sudo -i```
2. ```root@workeredteam:˜# apt-get update && apt-get upgrade -y```
3. ```root@workeredteam:˜# apt-get install -y docker.io```
4. ```root@workeredteam:˜# apt-get install -y vim```
5. ```root@workeredteam:˜# vim /etc/apt/sources.list.d/kubernetes.list```
> *deb http://apt.kubernetes.io/ kubernetes-xenial main*
6. ```root@workeredteam:˜# curl -s https://packages.cloud.google.com/apt/doc/apt-key.gpg | apt-key add -```
7. ```root@workeredteam:˜# apt-get update```
8. ```root@workeredteam:˜# apt-get install -y kubeadm=1.18.1-00 kubelet=1.18.1-00 kubectl=1.18.1-00```
9. ```root@workeredteam:˜# apt-mark hold kubeadm kubelet kubectl```
10. ```student@masteredteam:˜$ ip addr show```
11. ```student@masteredteam:˜$ sudo kubeadm token list```
12. ```root@workeredteam:˜# vim /etc/hosts```
13. ```root@workeredteam:˜# vim /etc/hosts```
> *10.128.0.3 k8smasteredteam #<-- Add this line* #Recuerden que esta IP es la del Master Node
> *127.0.0.1 localhost*
14. 




