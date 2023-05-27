# Mimir
A DataOps platform toolkit for Kubernetes

## Prerequisites

### Setup ArgoCD

- Create ArgoCD namespace
````bash
kubectl create namespace argocd
````

- Install ArgoCD
````bash
kubectl apply -n argocd -f https://raw.githubusercontent.com/argoproj/argo-cd/stable/manifests/install.yaml
````

- Switch the server service to LoadBalancer
````bash
kubectl patch svc argocd-server -n argocd -p '{"spec": {"type": "LoadBalancer"}}'
````

- Download ArgoCD client and move it in your PATH as argocd.exe
````bash
wget https://github.com/argoproj/argo-cd/releases/download/v2.7.2/argocd-windows-amd64.exe
````

- Retrieve the admin password
````bash
argocd admin initial-password -n argocd
````

## Installation

### Setup Rook

- Create Infrastructure project
````bash
kubectl apply -f https://raw.githubusercontent.com/Algueron/mimir/main/manifests/infrastructure-argo-project.yaml
````
- Create CertManager Application
````bash
kubectl apply -f https://raw.githubusercontent.com/Algueron/mimir/main/manifests/certmanager.yaml
````
- Create Rook Operator Application
````bash
kubectl apply -f https://raw.githubusercontent.com/Algueron/mimir/main/manifests/rook-operator.yaml
````
- Create Ceph Cluster Application
````bash
kubectl apply -f https://raw.githubusercontent.com/Algueron/mimir/main/manifests/ceph-cluster.yaml
````
