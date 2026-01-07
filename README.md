# Kubernetes Playground

A personal playground to experiment with Kubernetes concepts using Minikube.
This repository focuses on **hands-on commands** with brief conceptual notes.

## Installation

### Kubectl

- **kubectl**  
  Command-line tool to interact with Kubernetes clusters.  
  Install: https://kubernetes.io/docs/tasks/tools/

- **Minikube**  
  Runs a local, single-node Kubernetes cluster.  
  Install: https://minikube.sigs.k8s.io/docs/start/

## Installation Check

```bash
kubectl version
minikube version
```

## Commands

### Minikube

#### Start Minikube

```bash
# Initializes and launches local kubernetes cluster
minikube start

# Launch Kubernetes dashboard:
minikube dashboard --port=63840
```

#### Stop Minikube

Stops the running cluster without deleting it:

```bash
minikube stop
```

#### Deleting Minikube (⚠️ Destructive)

Deletes the old minikube clusters.

> Note: First stop running instance then execute following command

```bash
minikube delete
```

#### Minikube IP

```bash
minikube ip
```

#### Minikube Tunnel bind

```bash
minikube tunnel -c
```

For Linux

```bash
minikube tunnel --bind-address="127.0.0.1" -c
```

### Deploymnets

#### Viewing Deployments

```bash
kubectl get deployments
```

#### Deploying

```bash
kubectl create deployment <deployment-name> --image=<docker-image[:tag]>
```

- deployment-name: Any valid name, unique within a namespace
- docker-image: It would be a URL if we weren't hosting the image on Docker Hub, which is the default

#### Get Deployment

```bash
kubectl get deployment <deployment-name> -o yaml

# Get deplyment and write to file locally
kubectl get deployment synergychat-web -o yaml > web-deployment.yaml
```

#### Apply changes

```bash
kubectl apply -f web-deployment.yaml
```

#### Deleting Deployment

```bash
kubectl delete deployment <deployment-name>
```

#### Get Replica Sets

```bash
kubectl get replicasets
```

#### Editing deployment

```bash
kubectl edit deployment <deployment-name>
```

### Pods

#### Viewing Pods

Get a list of your running pods

```bash
kubectl get pods
```

Parameters

- `-o wide`: Give more columns

#### Deleting Pod manually

```bash
kubectl delete pod <pod-name>
```

- This will delete the pod, but as the configuration says `n` pods and by deleting we made the running instance count to `n-1`, so kubernetes start a new pod from the same template making the running instance again `n`. This feels like a restart.

#### Port forwarding

```bash
kubectl port-forward <pod-name> 8080:8080
```

- pod-name are your pod's name. Can be retrived uding `get pods` command

#### Print Logs of a pod

```bash
kubectl logs <pod-name>
```

Flags:
`--all-containers`: logs from all containers

### Config map

#### Get Config map

```bash
kubectl get configmaps
```

#### Delete Configmap

```bash
kubectl delete configmap <configmap-name>
```

### Service

#### Get Service

```bash
kubectl -n crawler get svc
# Or
kubectl get svc web-service -o yaml
```

#### Deleting Service

```bash
kubectl delete service <service-name>
```

### Gateway

#### Installing

Gateway API is just a spec and there are different implementations. The install instruction are for (Envoy Gateway)[https://gateway.envoyproxy.io/docs/concepts/]

```bash
kubectl apply --server-side -f https://github.com/envoyproxy/gateway/releases/download/v1.5.1/install.yaml
```

### Persistence Volumes

```bash
kubectl get pvc
kubectl get pv
```

#### Deleting PVC

```bash
kubectl delete pvc <pvc-name>
```

### Namespaces

Use the `--namespace` or `-n` flag with the command. If you don't then it will use the `default` namespace

The `kube-system` namespace is where all the core Kubernetes components live, it's created automatically when you install Kubernetes. You don't want to mess with it.

#### Get Namespace

```bash
kubectl get namespaces

# Shorter Version
kubectl get ns
```

#### Create New Namespace

```bash
kubectl create ns <namespace-name>
```

### Misc

#### Kubernetes Proxy

This will start a proxy server on your local machine

```bash
kubectl proxy
```
