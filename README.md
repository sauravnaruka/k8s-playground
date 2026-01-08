# Kubernetes Playground

Personal playground for experimenting with Kubernetes using Minikube. This is a collection of my most-used commands with brief notes — not meant to be comprehensive.

---

## Installation

**kubectl** — Command-line tool to interact with Kubernetes clusters
https://kubernetes.io/docs/tasks/tools/

**Minikube** — Runs a local, single-node Kubernetes cluster
https://minikube.sigs.k8s.io/docs/start/

**Verify installation:**
```bash
kubectl version
minikube version
```

---

## Minikube

### Start and Stop

```bash
# Start the local Kubernetes cluster
minikube start

# Launch the Kubernetes dashboard
minikube dashboard --port=63840

# Stop the cluster (preserves it)
minikube stop
```

### Delete Cluster ⚠️

Stop Minikube first, then delete:
```bash
minikube delete
```

### Networking

```bash
# Get Minikube IP
minikube ip

# Start tunnel (generic)
minikube tunnel -c

# Start tunnel (Linux)
minikube tunnel --bind-address="127.0.0.1" -c
```

---

## Deployments

```bash
# View all deployments
kubectl get deployments

# Create a deployment
kubectl create deployment <deployment-name> --image=<docker-image[:tag]>

# Get deployment details as YAML
kubectl get deployment <deployment-name> -o yaml

# Export deployment to file
kubectl get deployment <deployment-name> -o yaml > deployment.yaml

# Apply changes from file
kubectl apply -f deployment.yaml

# Edit deployment in editor
kubectl edit deployment <deployment-name>

# Delete a deployment
kubectl delete deployment <deployment-name>

# View replica sets
kubectl get replicasets
```

**Note:** `<deployment-name>` must be unique within a namespace. Images default to Docker Hub.

---

## Pods

```bash
# List pods
kubectl get pods
kubectl get pods -o wide  # More details

# Delete a pod
kubectl delete pod <pod-name>
```

**Note:** Deleting a pod triggers Kubernetes to start a replacement (like a restart).

### Working with Pods

```bash
# Forward local port to pod
kubectl port-forward <pod-name> 8080:8080

# View pod logs
kubectl logs <pod-name>
kubectl logs <pod-name> --all-containers  # All containers in pod
```

---

## ConfigMaps

```bash
# List config maps
kubectl get configmaps

# Delete a config map
kubectl delete configmap <configmap-name>
```

---

## Services

```bash
# List services
kubectl get svc
kubectl get svc -n <namespace>  # In specific namespace

# Get service details
kubectl get svc <service-name> -o yaml

# Delete a service
kubectl delete service <service-name>
```

---

## Persistence

```bash
# List persistent volume claims
kubectl get pvc

# List persistent volumes
kubectl get pv

# Delete a PVC
kubectl delete pvc <pvc-name>
```

---

## Namespaces

Use `-n <namespace>` or `--namespace <namespace>` with commands. Defaults to `default` namespace if not specified.

The `kube-system` namespace contains core Kubernetes components — avoid modifying it.

```bash
# List namespaces
kubectl get namespaces
kubectl get ns  # Shorter

# Create namespace
kubectl create ns <namespace-name>
```

---

## Metrics

```bash
# Enable metrics server (Minikube addon)
minikube addons enable metrics-server

# Verify metrics server is running
kubectl -n kube-system get pod

# View resource usage per pod
kubectl top pod
```

---

## Gateway API

Gateway API is a spec with multiple implementations. Below uses [Envoy Gateway](https://gateway.envoyproxy.io/docs/concepts/).

```bash
# Install Envoy Gateway
kubectl apply --server-side -f https://github.com/envoyproxy/gateway/releases/download/v1.5.1/install.yaml
```

---

## Utilities

```bash
# Start local proxy server
kubectl proxy
```
