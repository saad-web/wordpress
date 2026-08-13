# WordPress on Kubernetes with ArgoCD

This repository contains Kubernetes manifests for deploying WordPress with MySQL, managed by ArgoCD.

## Components

- **MySQL**: Database backend with persistent storage
- **WordPress**: WordPress application with persistent storage
- **Services**: ClusterIP for MySQL, NodePort for WordPress
- **Ingress**: Optional ingress for external access

## Deployment

### Prerequisites
- Kubernetes cluster
- ArgoCD installed
- Storage class available for PVCs

### Deploy with ArgoCD

1. Apply the ArgoCD application:
```bash
kubectl apply -f argocd-application.yaml
```

2. ArgoCD will automatically sync and deploy all manifests

### Access WordPress

- **NodePort**: http://<node-ip>:30080
- **Ingress**: http://wordpress.local (if ingress controller is configured)

## GitOps Workflow

1. Make changes to manifests in `manifests/` directory
2. Push to `main` branch
3. ArgoCD automatically detects and syncs changes
4. GitHub Actions validates manifests on push

## Structure

```
.
├── manifests/
│   ├── 00-namespace.yaml
│   ├── 01-mysql-secret.yaml
│   ├── 02-mysql-pvc.yaml
│   ├── 03-mysql-deployment.yaml
│   ├── 04-mysql-service.yaml
│   ├── 05-wordpress-pvc.yaml
│   ├── 06-wordpress-deployment.yaml
│   ├── 07-wordpress-service.yaml
│   └── 08-wordpress-ingress.yaml
├── .github/workflows/
│   └── deploy.yaml
├── argocd-application.yaml
└── README.md
```
