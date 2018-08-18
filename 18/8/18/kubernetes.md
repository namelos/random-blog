# Kubernetes

## Minicube and Kubectl

* Minicube is a simple way to try kubernetes on a single node.
* Google Kubernetes Engine (GKE) is a much easier way to get multi node environment instead of setting up too much network stuff.

## Trouble shooting on error 126
By default minikube searches for virtual box. If you partially deleted virtual box this may happen.
To fix this you need to remove all stuff like `/usr/local/bin/VBox*` and `/usr/local/bin/vbox*`, then start minikube with:
```sh
minikube start --vm-driver=xhyve
```
