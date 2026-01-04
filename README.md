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

#### Get Replica Sets

```bash
kubectl get replicasets
```

#### Get Config map

```bash
kubectl get configmaps
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

### Misc

#### Kubernetes Proxy

This will start a proxy server on your local machine

```bash
kubectl proxy
```
