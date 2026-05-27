# Kubernetes GitOps Course Project

## About Project

This project demonstrates deployment of a stateful application in Kubernetes using GitOps approach.

Application: Redmine  
Database: PostgreSQL  
Database Operator: CloudNativePG  
GitOps: FluxCD  
Package manager: Helm

---

# Environments

## Staging

Namespace: `staging`

- 1 Redmine pod
- 1 PostgreSQL instance
- HTTPS enabled
- Domain:
  - https://redmine.staging.local

---

## Production

Namespace: `production`

- HPA enabled
- 2-5 Redmine replicas
- 2 PostgreSQL instances
- HTTPS enabled
- Domain:
  - https://redmine.local

---

# Technologies

- Kubernetes
- FluxCD
- Helm
- CloudNativePG
- PostgreSQL
- Redmine
- Traefik Ingress
- HPA
- Self-signed TLS

---

# Repository Structure

```text
apps/
charts/
certs/
clusters/
infrastructure/
screenshots/
```

---

# Flux Verification

```bash
flux get helmreleases -A
flux get kustomizations -A
```

---

# PostgreSQL Verification

```bash
kubectl get clusters.postgresql.cnpg.io -A
```

---

# HPA Verification

```bash
kubectl get hpa -n production
```

---

# Self-Healing Test

Deployment was manually deleted:

```bash
kubectl delete deploy redmine -n staging
```

Deployment was restored using Flux reconciliation:

```bash
flux reconcile helmrelease redmine -n staging --with-source
```

---

# Screenshots

Project screenshots and verification results are available in the `screenshots/` directory.
