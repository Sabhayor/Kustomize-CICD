# Kustomize with CI/CD Pipelines

## Overview
This lesson introduces how to automate Kubernetes configuration management using **Kustomize** integrated into a **GitHub Actions CI/CD pipeline**. You will progress from a basic working pipeline to handling complex configurations and applying best practices, especially in cloud environments such as AWS.

## Integrating Kustomize into CI/CD Pipelines

### Objective
Automate Kubernetes deployments using Kustomize through GitHub Actions.

---

## Step 1: Repository Structure

```
.
├── .github/
│   └── workflows/
│       └── main.yml
├── base/
│   └── kustomization.yaml
└── overlays/
    └── production/
        └── kustomization.yaml
```

---

## Step 2: GitHub Actions Workflow

Create `.github/workflows/main.yml`

```yaml
name: Deploy with Kustomize
on:
  push:
    branches:
      - main

jobs:
  deploy:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v2
      - uses: azure/setup-kubectl@v1
      - uses: imranismail/setup-kustomize@v1
      - name: Deploy
        run: kubectl apply -k overlays/production
```

---

## Step 3: Cluster Access
Ensure GitHub Actions can access your cluster using kubeconfig or cloud-native authentication.

---

## Step 4: Test the Pipeline
Commit a change and push to main:

```bash
git add .
git commit -m "Update config"
git push origin main
```

Check the **Actions** tab to confirm deployment.

---

## Handling Complex Configurations
- Use base and overlays
- Separate apps and environments
- Apply patches and generators

---

## Best Practices
- Use ConfigMaps and Secrets
- Avoid hardcoding values
- Review changes with pull requests
- Test in staging first

