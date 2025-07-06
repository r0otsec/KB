---
tags:
  - technologies
date: 2023-09-1
---
- Open source container orchestration platform.
- Automates deployment, scaling and management of containerized apps.
# Components

- `Kubernetes cluster` is made up of two parts:
	- `Control Plane`: brain of the cluster (makes global decisions like scheduling).
	- `Worker Nodes`: machines where containers (pods) run.
# Control Plane Components

- Run on the master node(s) and manage cluster's desired state:
	- `kube-apiserver`: central access point for interaction with cluster.
		- exposes the Kubernetes API and all commands (e.g. `kubectl`) talk to it.
	- `etcd`: distributed key-value store that persists all cluster data.
		- config, states, secrets and metadata.
	- `kube-scheduler`: assigns new pods to nodes by evaluating resource availability, policies and constraints.
	- `kube-controller-manager`: runs background loops that track cluster's state.
	- `cloud-controller-manager`: handles integration with cloud services like load balancers/storage.
# Worker Node Components

- Where the actual apps run:
	- `kubelet`: talks to control plane - ensuring containers are running healthily.
	- `kube-proxy`: maintains network rules to allow comms to and from pods/services.
	- `Container runtime`: software that runs containers:
		- e.g. `containerd`, `CRI-O` or formerly [[Docker]].
# How It Works

- A basic workflow is:
	- user applies a YAML manifest using `kubectl apply -f`.
	- `kube-apiserver` receives request and stores it in `etcd`.
	- scheduler assigns the pod to a node.
	- `kubelet` on the node pulls the container image and starts pod.
	- `kube-proxy` updates network rules to make pod accessible.

For example:

```yaml
# nginx-deployment.yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: nginx-deploy
spec:
  replicas: 2
  selector:
    matchLabels:
      app: nginx
  template:
    metadata:
      labels:
        app: nginx
    spec:
      containers:
      - name: nginx
        image: nginx:latest
        ports:
        - containerPort: 80
```

And some commands:

```bash
kubectl apply -f nginx-deployment.yaml
kubectl get pods
kubectl expose deployment nginx-deploy --type=NodePort --port=80
kubectl get svc
```