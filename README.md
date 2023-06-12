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
kubectl apply -f https://raw.githubusercontent.com/Algueron/mimir/main/manifests/infrastructure/infrastructure-argo-project.yaml
````
- Install and Configure Rook
````bash
kubectl apply -f https://raw.githubusercontent.com/Algueron/mimir/main/manifests/infrastructure/rook-application.yaml
````
- Retrieve the admin password
````bash
kubectl -n rook-ceph get secret rook-ceph-dashboard-password -o jsonpath="{['data']['password']}" | base64 --decode && echo
````
