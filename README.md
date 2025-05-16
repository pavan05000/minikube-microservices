# Minikube Microservices Project

This is a local Kubernetes setup using Minikube where I deployed three microservices and a MinIO storage service using Helm charts.

## Services included:
- **auth-service**: Handles authentication
- **data-service**: Handles data processing/storage
- **gateway**: Acts as API gateway for the microservices
- **minio**: S3 compatible object storage service


## How I Deployed

1. Created **app namespace** in Minikube  
   ```bash
   kubectl create namespace app
Installed MinIO for storage

kubectl apply -f minio-deployment.yaml
kubectl apply -f minio-service.yaml
Installed Helm charts for each service inside app namespace:

helm install auth-service ./charts/auth-service -n app
helm install data-service ./charts/data-service -n app
helm install gateway ./charts/gateway -n app
Verified pods and services are running

kubectl get all -n app
How to Access
Services expose ClusterIP internally on port 80

To access from your machine, you can setup port-forward or configure Ingress

Example port-forward for gateway:

kubectl port-forward svc/gateway 8080:80 -n app
Then open http://localhost:8080

Notes
Used Helm templates for easy management

Configured readiness and liveness probes for each deployment

MinIO deployed as separate service in minio namespace

All resources are deployed in app namespace for separation
