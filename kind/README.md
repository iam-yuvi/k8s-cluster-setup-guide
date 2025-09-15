# 🚀 Kubernetes in Docker (Kind) Setup Guide

This repository provides a step-by-step guide to install **Docker**, **kubectl**, and **Kind** on Ubuntu, and then create a Kubernetes cluster.

---

## 📋 Prerequisites
- Ubuntu 20.04 / 22.04 / 24.04 (works on VM, EC2, or bare metal)
- At least **2 CPUs**, **2 GB RAM**, **10 GB disk**
- Internet access

---

## 🔧 Installation Steps

### 1. Update System
```bash
sudo apt update && sudo apt upgrade -y
```

2. Install Docker
```bash
sudo apt install -y docker.io
sudo systemctl enable docker --now
docker --version
```

3. Install kubectl
```bash
curl -Lo kubectl https://dl.k8s.io/release/$(curl -s -L https://dl.k8s.io/release/stable.txt)/bin/linux/amd64/kubectl
chmod +x kubectl
sudo mv kubectl /usr/local/bin/
```

verify:
```bash
kubectl version --client
```
4. Install Kind
```bash
curl -Lo kind https://kind.sigs.k8s.io/dl/latest/kind-linux-amd64
chmod +x kind
sudo mv kind /usr/local/bin/
```

verify
```bash
kind --version
```
🚀 Create a Kubernetes Cluster
Create a cluster named my-cluster:

```bash

kind create cluster --name my-cluster
```

Verify the cluster:

```bash
kubectl cluster-info
kubectl get nodes
```

Expected output:

pgsql
Copy code
NAME                       STATUS   ROLES           AGE   VERSION
my-cluster-control-plane   Ready    control-plane   1m    v1.xx.x

🧪 Deploy a Test App (Optional)
Deploy Nginx:

```bash
kubectl create deployment nginx --image=nginx
kubectl expose deployment nginx --port=80 --type=NodePort
kubectl get svc nginx
```

You now have a running Nginx service inside your Kind cluster 🎉

✅ Summary
Installed Docker, kubectl, and Kind

Created a single-node Kubernetes cluster

Verified the cluster with kubectl

(Optional) Deployed a test Nginx app
