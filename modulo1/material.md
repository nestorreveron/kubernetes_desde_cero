# Material de apoyo módulo 1

[Presentación del Módulo 1](https://1drv.ms/p/s!AoX_zvfKf0RXj8g35ppcFemsnZdOew?e=yT8mrP "Presentación")

1. **Origen de Kubernetes**: https://kube.academy/courses/getting-started/lessons/the-origin-of-kubernetes 

2. **Borg**: https://kubernetes.io/blog/2015/04/borg-predecessor-to-kubernetes/ 

3. **Kubernetes wiki**: https://en.wikipedia.org/wiki/Kubernetes 

4. **CNCF (Cloud Native Computing Foundation)**: https://www.cncf.io/projects/ 

5. **Berkeley Software Distribution**: https://en.wikipedia.org/wiki/Berkeley_Software_Distribution 

6. **CHROOT**: https://en.wikipedia.org/wiki/Chroot 

7. **FreeBSD**: https://en.wikipedia.org/wiki/FreeBSD

8. **FreeBSD jail**: https://en.wikipedia.org/wiki/FreeBSD_jail

9. **Join us in celebrating 30 years of Linux**: https://linuxfoundation.org/linux30th/ 

10. **Linux namespaces**: https://en.wikipedia.org/wiki/Linux_namespaces

11. **Linux Cgroups - Control Groups**: https://en.wikipedia.org/wiki/Cgroups 

12. **Solaris Containers**: https://en.wikipedia.org/wiki/Solaris_Containers

13. **LXC**: https://en.wikipedia.org/wiki/LXC 

14. **Google lmctfy**: https://en.wikipedia.org/wiki/Lmctfy / https://github.com/google/lmctfy 

15. **Docker**: https://en.wikipedia.org/wiki/Docker_(software)

16. **APPC**: https://github.com/appc/spec

17. **OCI**: https://opencontainers.org/

18. **kata Containers**: https://katacontainers.io/learn/

19. **gVisor**: https://github.com/google/gvisor

20. **Podman**: https://podman.io/ 

21. **Containerd**: https://www.cncf.io/projects/containerd/


## Manifiesto para el deploymento del punto 1.4: Azure Vote App 
```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: azure-vote-back
spec:
  replicas: 1
  selector:
    matchLabels:
      app: azure-vote-back
  template:
    metadata:
      labels:
        app: azure-vote-back
    spec:
      nodeSelector:
        "kubernetes.io/os": linux
      containers:
      - name: azure-vote-back
        image: mcr.microsoft.com/oss/bitnami/redis:6.0.8
        env:
        - name: ALLOW_EMPTY_PASSWORD
          value: "yes"
        resources:
          requests:
            cpu: 100m
            memory: 128Mi
          limits:
            cpu: 250m
            memory: 256Mi
        ports:
        - containerPort: 6379
          name: redis
---
apiVersion: v1
kind: Service
metadata:
  name: azure-vote-back
spec:
  ports:
  - port: 6379
  selector:
    app: azure-vote-back
---
apiVersion: apps/v1
kind: Deployment
metadata:
  name: azure-vote-front
spec:
  replicas: 1
  selector:
    matchLabels:
      app: azure-vote-front
  template:
    metadata:
      labels:
        app: azure-vote-front
    spec:
      nodeSelector:
        "kubernetes.io/os": linux
      containers:
      - name: azure-vote-front
        image: mcr.microsoft.com/azuredocs/azure-vote-front:v1
        resources:
          requests:
            cpu: 100m
            memory: 128Mi
          limits:
            cpu: 250m
            memory: 256Mi
        ports:
        - containerPort: 80
        env:
        - name: REDIS
          value: "azure-vote-back"
---
apiVersion: v1
kind: Service
metadata:
  name: azure-vote-front
spec:
  type: LoadBalancer
  ports:
  - port: 80
  selector:
    app: azure-vote-front
    
```


    
    

