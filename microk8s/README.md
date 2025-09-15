# 🚀 MicroK8s Setup Guide (Single Node Kubernetes Cluster)

This guide explains how to install and configure **MicroK8s** on Ubuntu to run a lightweight single-node Kubernetes cluster.  

---

## 📋 Prerequisites
- Ubuntu 20.04 / 22.04 / 24.04 (VM, EC2, or bare metal)
- At least **2 CPUs**, **2 GB RAM**, **10 GB disk**
- Internet access
- User with `sudo` privileges

---

## 🔧 Installation Steps

### 1. Update System
```bash
sudo apt update && sudo apt upgrade -y
```
### 2. Install MicroK8s
```bash
sudo snap install microk8s --classic --channel=1.30/stable
```
👉 Replace 1.30 with the latest Kubernetes version if needed.

### 3. Add User to MicroK8s Group
```bash
sudo usermod -aG microk8s $USER
mkdir -p ~/.kube
sudo chown -R $USER ~/.kube
newgrp microk8s
```

### 4. Verify Installation
Check MicroK8s status:

```bash
microk8s status --wait-ready
```

Expected output:
microk8s is running

Check nodes:

```bash
microk8s kubectl get nodes
```
Output should show your node as Ready.

### ⚙️ Enable Useful Add-ons
Enable common Kubernetes add-ons:

```bash
microk8s enable dns dashboard ingress hostpath-storage
```

Verify add-ons:

```bash
microk8s status
```

## 🚀 Deploy a Test Application

### 1. Create Deployment
```bash
microk8s kubectl create deployment nginx --image=nginx
```
### 2. Expose Deployment
```bash
microk8s kubectl expose deployment nginx --port=80 --type=NodePort
```
### 3. Check Service
```bash
microk8s kubectl get svc nginx
```
You’ll see a NodePort (e.g., 30080).

### 4. Access the App
On localhost:

```bash
curl http://127.0.0.1:<NodePort>
```
On VM/EC2:

```bash
curl http://<your-public-ip>:<NodePort>
```

### ✅ Summary
Installed MicroK8s on Ubuntu

Configured user access and verified cluster readiness

Enabled DNS, Dashboard, Ingress, and Storage add-ons

Deployed and accessed an Nginx application
