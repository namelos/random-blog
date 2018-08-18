# Kubernetes
The following content are some notes from the book *Kubernetes in Action*, Manning publications.

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

## Trouble shooting on error 126
By default minikube searches for virtual box. If you partially deleted virtual box this may happen.
To fix this you need to remove all stuff like `/usr/local/bin/VBox*` and `/usr/local/bin/vbox*`, then start minikube with:
```sh
minikube start --vm-driver=xhyve
```
