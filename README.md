# Rotate GHCR imagePullSecrets – GitHub Actions Template

## Overview

This GitHub Actions workflow rotates or updates a **GHCR Docker registry secret** across multiple Kubernetes namespaces in a GKE cluster. It is designed as a reusable template for securely managing image pull secrets.

The workflow:

* Authenticates to GKE
* Connects to the Kubernetes cluster
* Creates or updates the `ghcr-secret` in specified namespaces
* Supports manual approval via GitHub Environments

---

## Workflow Features

* Manual trigger via GitHub Actions UI
* Multi-namespace secret rotation
* Idempotent secret update (create or replace)
* GKE authentication via service account
* Environment approval support

---

## Required GitHub Secrets

Configure the following repository secrets:

```
GKE_KEY          # GCP service account JSON key
GHCR_USERNAME    # GitHub Container Registry username
GHCR_PAT         # GitHub personal access token
```

---

## Setup

### 1. Add Workflow File

Create the workflow file:

```
.github/workflows/rotate-secret.yaml
```

Paste the workflow YAML into this file.

---

### 2. Configure Environment Approval (Optional)

1. Go to **Repository → Settings → Environments**
2. Create an environment named:

```
prod
```

3. Add **Required reviewers** to enforce approval before execution for authorized runs

---

## Usage

### Trigger the Workflow

1. Go to **Actions → Rotate GHCR imagePullSecrets**
2. Click **Run workflow**
3. Enter namespaces as comma-separated values:

```
dev,staging,prod
```

---

## Behavior

For each namespace:

* If `ghcr-secret` does not exist → it is created
* If it already exists → it is updated with new credentials

This ensures consistent secret rotation across environments.

---

## Customization

You should modify:

* Cluster name and region in the workflow
* Secret name
* Docker registry settings
* Namespace input handling

---
