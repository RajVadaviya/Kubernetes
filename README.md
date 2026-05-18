# Kubernetes Zero to Hero 🚀

A beginner-friendly Kubernetes repository for learning Kubernetes practically using Minikube on AWS EC2.

This repository is created to help beginners understand:

* Kubernetes basics
* Pods
* Deployments
* ReplicaSets
* Services
* YAML files
* kubectl commands
* Minikube setup
* Docker integration

---

# 📌 Prerequisites

Before starting, create:

* AWS Account
* Ubuntu EC2 Instance
* Security Group with SSH (Port 22)

Recommended EC2 Instance:

* `c7i-flex.large`
  OR
* `t3.medium`

Minimum Recommended:

* 2 vCPU
* 4 GB RAM

---

# 📌 Connect To EC2

```bash
ssh -i your-key.pem ubuntu@YOUR_PUBLIC_IP
```

---

# 📌 Step 1 — Update System

```bash
sudo apt update && sudo apt upgrade -y
```

---

# 📌 Step 2 — Install Docker

```bash
sudo apt install docker.io -y
```

Start Docker:

```bash
sudo systemctl start docker
```

Enable Docker:

```bash
sudo systemctl enable docker
```

Add current user to Docker group:

```bash
sudo usermod -aG docker $USER
```

Apply changes:

```bash
newgrp docker
```

Verify Docker:

```bash
docker --version
```

Test Docker:

```bash
docker run hello-world
```

---

# 📌 Step 3 — Install kubectl

Install dependencies:

```bash
sudo apt-get install -y apt-transport-https ca-certificates curl gnupg
```

Add Kubernetes key:

```bash
curl -fsSL https://pkgs.k8s.io/core:/stable:/v1.30/deb/Release.key | \
sudo gpg --dearmor -o /etc/apt/keyrings/kubernetes-apt-keyring.gpg
```

Add Kubernetes repository:

```bash
echo 'deb [signed-by=/etc/apt/keyrings/kubernetes-apt-keyring.gpg] https://pkgs.k8s.io/core:/stable:/v1.30/deb/ /' | \
sudo tee /etc/apt/sources.list.d/kubernetes.list
```

Update packages:

```bash
sudo apt update
```

Install kubectl:

```bash
sudo apt install -y kubectl
```

Verify:

```bash
kubectl version --client
```

---

# 📌 Step 4 — Install Minikube

Download Minikube:

```bash
curl -LO https://github.com/kubernetes/minikube/releases/latest/download/minikube-linux-amd64
```

Install Minikube:

```bash
sudo install minikube-linux-amd64 /usr/local/bin/minikube
```

Verify:

```bash
minikube version
```

---

# 📌 Step 5 — Start Kubernetes Cluster

```bash
minikube start --driver=docker
```

Verify cluster:

```bash
kubectl get nodes
```

Expected Output:

```text
NAME       STATUS   ROLES           AGE   VERSION
minikube   Ready    control-plane
```

---

# 📌 Kubernetes Architecture

## Docker

Docker helps us build and run containers.

## Kubernetes

Kubernetes helps us manage containers at scale.

## Minikube

Minikube creates a local Kubernetes cluster.

## kubectl

kubectl is the command-line tool used to interact with Kubernetes.

---

# 📌 Create First Pod

Create nginx pod:

```bash
kubectl run nginx --image=nginx
```

Check pods:

```bash
kubectl get pods
```

Detailed view:

```bash
kubectl get pods -o wide
```

---

# 📌 Deployment YAML Example

Create file:

```bash
vim deployment.yaml
```

Paste:

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: nginx-deployment
  labels:
    app: nginx
spec:
  replicas: 3
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
        image: nginx:1.14.2
        ports:
        - containerPort: 80
```

Apply deployment:

```bash
kubectl apply -f deployment.yaml
```

Check deployment:

```bash
kubectl get deployment
```

Check replicas:

```bash
kubectl get rs
```

Check pods:

```bash
kubectl get pods
```

---

# 📌 Scaling Deployment

Scale replicas:

```bash
kubectl scale deployment nginx-deployment --replicas=5
```

Verify:

```bash
kubectl get pods
```

---

# 📌 Delete Deployment

```bash
kubectl delete deployment nginx-deployment
```

---

# 📌 Useful kubectl Commands

Check nodes:

```bash
kubectl get nodes
```

Check pods:

```bash
kubectl get pods
```

Check all namespaces:

```bash
kubectl get pods -A
```

Describe pod:

```bash
kubectl describe pod POD_NAME
```

Check logs:

```bash
kubectl logs POD_NAME
```

Delete pod:

```bash
kubectl delete pod POD_NAME
```

---

# 📌 Minikube Commands

Check status:

```bash
minikube status
```

SSH into Minikube:

```bash
minikube ssh
```

Stop cluster:

```bash
minikube stop
```

Delete cluster:

```bash
minikube delete
```

---

# 📌 Troubleshooting

## Issue: kubectl connection refused

Reason:

* Kubernetes cluster not started.

Solution:

```bash
minikube start --driver=docker
```

---

## Issue: insufficient memory

Reason:

* EC2 instance RAM too low.

Recommended:

* 4 GB RAM
* c7i-flex.large
* t3.medium

---

## Issue: Docker not found

Install Docker:

```bash
sudo apt install docker.io -y
```

---

# 📌 Recommended Learning Order

1. Docker Basics
2. Pods
3. Deployments
4. ReplicaSets
5. Services
6. Namespaces
7. ConfigMaps
8. Secrets
9. Ingress
10. Helm

---

# 📌 GitHub Push Commands

Initialize Git:

```bash
git init
```

Add files:

```bash
git add .
```

Commit:

```bash
git commit -m "Initial Kubernetes project"
```

Add GitHub repository:

```bash
git remote add origin YOUR_GITHUB_REPO_LINK
```

Push:

```bash
git push -u origin main
```

---

# 📌 Author

Raj Vadaviya

Learning Cloud & DevOps 🚀
