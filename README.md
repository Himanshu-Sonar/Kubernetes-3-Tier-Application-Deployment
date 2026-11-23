# Kubernetes 3-Tier Application Deployment

## Project Overview

This project demonstrates the deployment of a 3-tier application architecture using Kubernetes. It consists of frontend, backend, and admin components, deployed using Kubernetes Deployments and exposed internally through ClusterIP Services.

NGINX Ingress Controller is configured to route incoming HTTP requests to the respective Services based on URL paths.

## Architecture

**Request Flow:**

Browser → NGINX Ingress Controller → Kubernetes Services → Application Pods

| Component | Kubernetes Resource | Replicas | Container Port |
|---|---|---:|---:|
| Frontend | Deployment + ClusterIP Service | 2 | 80 |
| Backend | Deployment + ClusterIP Service | 2 | 5678 |
| Admin | Deployment + ClusterIP Service | 2 | 5678 |

## Routing Configuration

| URL Path | Destination |
|---|---|
| `/` | frontend-service |
| `/api` | backend-service |
| `/admin` | admin-service |

The Ingress configuration uses path-based routing without a hostname restriction.

## Technologies Used

- Kubernetes
- Docker Containers
- NGINX Ingress Controller
- YAML
- kubectl
- Killercoda Kubernetes Playground

## Project Structure

```text
Kubernetes-3-Tier-Application-Deployment/
├── k8s/
│   ├── frontend-deployment.yaml
│   ├── backend-deployment.yaml
│   ├── admin-deployment.yaml
│   ├── frontend-service.yaml
│   ├── backend-service.yaml
│   ├── admin-service.yaml
│   └── ingress.yaml
├── screenshots/
└── README.md
```

## Deployment Instructions

### 1. Clone the repository

```bash
git clone YOUR_REPOSITORY_URL
cd Kubernetes-3-Tier-Application-Deployment
```

### 2. Apply Deployments

```bash
kubectl apply -f k8s/frontend-deployment.yaml
kubectl apply -f k8s/backend-deployment.yaml
kubectl apply -f k8s/admin-deployment.yaml
```

### 3. Apply Services

```bash
kubectl apply -f k8s/frontend-service.yaml
kubectl apply -f k8s/backend-service.yaml
kubectl apply -f k8s/admin-service.yaml
```

### 4. Apply Ingress

Ensure the NGINX Ingress Controller is installed.

```bash
kubectl apply -f k8s/ingress.yaml
```

### 5. Verify resources

```bash
kubectl get pods
kubectl get deployments
kubectl get services
kubectl get ingress
```

## Testing

Test the three routes through the configured Ingress endpoint:

```bash
curl http://INGRESS_ADDRESS:PORT/
curl http://INGRESS_ADDRESS:PORT/api
curl http://INGRESS_ADDRESS:PORT/admin
```

Expected results:

- `/` – NGINX Welcome Page
- `/api` – Hello from backend
- `/admin` – Hello from admin

## Key Learning Outcomes

- Deploying multi-component applications using Kubernetes.
- Managing application replicas with Deployments.
- Exposing Pods through ClusterIP Services.
- Configuring path-based routing using NGINX Ingress.
- Writing and applying Kubernetes YAML manifests.
- Managing and troubleshooting resources using kubectl.

## Environment

Developed and tested using the Killercoda Kubernetes Playground.

**Note:** The backend and admin components use HTTP echo containers for demonstration purposes. This project focuses on Kubernetes deployment, service discovery, and Ingress routing rather than a production-ready business application.
