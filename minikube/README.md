# 📝 Minikube Setup Documentation (Ubuntu 24.04)

This guide explains how to install and configure Minikube, Docker, and kubectl to run a local Kubernetes cluster.

---

## 1. System Requirements

- Ubuntu 22.04 / 24.04 (works on EC2, VM, or bare metal)
- Minimum 2 CPUs, 2 GB RAM, 20 GB disk
- Internet access

---

## 2. Install Dependencies

Install Docker
```bash
sudo apt-get update -y
sudo apt-get install -y docker.io
sudo systemctl enable --now docker
```

Add your user to the docker group (to avoid root issues):
```bash
sudo usermod -aG docker $USER
newgrp docker
```
Verify Docker:
```bash
docker ps
```

## 3. Install Minikube
```bash
curl -LO https://github.com/kubernetes/minikube/releases/latest/download/minikube-linux-amd64
sudo install minikube-linux-amd64 /usr/local/bin/minikube
rm minikube-linux-amd64
```

Verify Minikube:
```bash
minikube version
```

## 4. Install kubectl

Download latest stable kubectl binary:

```bash
curl -LO "https://dl.k8s.io/release/$(curl -s -L https://dl.k8s.io/release/stable.txt)/bin/linux/amd64/kubectl"
chmod +x kubectl
sudo mv kubectl /usr/local/bin/
```

Verify kubectl:
```bash
kubectl version --client
```

## 5. Start Minikube

Start a Kubernetes cluster using Docker driver:

```bash
minikube start --driver=docker
```

⚠️ If system has < 4GB RAM, allocate less memory:
```bash
minikube start --driver=docker --memory=2048mb --cpus=2
```
## 6. Verify Cluster

Check cluster status:
```bash
minikube status
```

Get all pods:
```bash
kubectl get pods -A
```

Check nodes:
```bash
kubectl get nodes
```
## 7. Cleanup & Reset

Stop cluster:
```bash
minikube stop
```

Delete cluster:
```bash
minikube delete --all
```
