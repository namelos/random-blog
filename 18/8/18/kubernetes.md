# Kubernetes
The following content are some poor notes from the book *Kubernetes in Action*, Manning publications.

## Minicube and Kubectl
* Minicube is a simple way to try kubernetes on a single node.
* Google Kubernetes Engine (GKE) is a much easier way to get multi node environment instead of setting up too much network stuff.

## Deploying your docker image

say you already have an image named `kubia`:
```sh
$ kubectl run kubia --image=namelosw/kubia --port=8080 --generator=run/v1
replicationcontroller "kubia" created
```

### Pods
Pods is a group of co-located containers. To list pods:

```sh
$ kubectl get pods
NAME          READY     STATUS              RESTARTS   AGE
kubia-gc4w6   0/1       ContainerCreating   0          43s
```

So it's still pending and pulling image when created `replicationcontroller`. After finish it will run:

```sh
$ kubectl get pods
NAME          READY     STATUS    RESTARTS   AGE
kubia-gc4w6   1/1       Running   0          7m
```

## Accessing application

Try to `curl` it:
```sh
$ curl localhost:8080
curl: (7) Failed to connect to localhost port 8080: Connection refused
```

So it's not yet exposed. Then try to expose it with:
```sh
$ kubectl expose rc kubia --type=LoadBalancer --name kubia-http
service "kubia-http" exposed
```

Try to inspect this `kubia-http` by `kubectl get services`:
```sh
$ kubectl get services
NAME         TYPE           CLUSTER-IP   EXTERNAL-IP   PORT(S)          AGE
kubernetes   ClusterIP      10.0.0.1     <none>        443/TCP          51m
kubia-http   LoadBalancer   10.0.0.97    <pending>     8080:32732/TCP   55s
```

It takes quite a time for load balancer to be created by the GKE.  
If you are using minikube, it does not support `LoadBalancer` and it will never assign external IP.  
However you can still use external port to access it.  
If you are using GKE you're good to use external IP already.  

For minikube:
```sh
$ minikube service kubia-http
http://192.168.64.2:32732/
# actually it will directly open browser
```

## Trouble shooting on error 126
By default minikube searches for virtual box. If you partially deleted virtual box this may happen.  
To fix this you need to remove all stuff like `/usr/local/bin/VBox*` and `/usr/local/bin/vbox*`, then start minikube with:
```sh
minikube start --vm-driver=xhyve
```
