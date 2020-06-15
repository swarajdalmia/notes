# Kubernetes 

- A container orchestration software. 

Creating multiple instances:
```
kubectl run --replicas=1000 my-web-server
```

- One can configure kubertes to automatically reduce/increase replicas depending on the load. A command to scale up to 2000:
```
kubectl scale --replicas=2000 my-web-server
```

- One can provide rolling updates:
```
kubectl rolling-update my-web-server --image=web-server-2
```

- and a roll back of updates as well:
```
kubectl rolling-update my-web-server --rollback
```

- It can provide testing of new features, by upgrading only a percentage of the applications through A,B testing methods.

- Kubernetes has high support for different storage, network, security tools/services.

## Kubernetes and Docker 

Kubernetes uses docker hosts to hosts and orchestrate container. It also supports rocket or cryo, and the host doesn't have to necessarily support docker. 

## Nodes

A node is a worker machine where containers are launched by kubernetes. A cluster is a set of nodes grouped together. The master watches over the nodes in the cluster and is responsible for the orchestration. 

## Components 

When kubernetes is intalled, the following components are installed as well : API server(front end for kubernetes), etcd server(distributed reliable key value store, responsible for logs to ensure there are no conflicts), kubelet(runs within each of the nodes), scheduler(respinsible for distributing work) controller(brain behind the orchestration), container runtime(docker or others).

## Some Simple Commands

- kubectl : the kubernetes CLI, used to manage the cluster. 

- `kubectl run` : to run the cluster
- `kubectl cluster-info` : to provide information about the cluster 
- `kubectl get nodes` : provide information about the nodes in the cluster




