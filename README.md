# Kubernetes-Tracker

This repository contains shared configurations, environment templates, and reusable GitHub Actions workflows for the **Kubernetes Incident Manager** organization.

## Contents
* `.github/workflows/reusable-ci.yml`: Reusable GitHub Actions workflow to build and push dockerized microservices to Azure Container Registry (ACR).
* `.env`: Template/local environment file with Azure Credentials.

## How to use Reusable Workflows
Add a `ci.yml` file to the microservice repository under `.github/workflows/` calling this workflow:

```yaml
name: CI Build and Push

on:
  push:
    branches:
      - main
  workflow_dispatch:

jobs:
  build-and-push:
    uses: Kubernetes-Incident-Manager/Kubernetes-Tracker/.github/workflows/reusable-ci.yml@main
    with:
      image_name: <service-image-name>
    secrets:
      ACR_LOGIN_SERVER: ${{ secrets.ACR_LOGIN_SERVER }}
      ACR_USERNAME: ${{ secrets.ACR_USERNAME }}
      ACR_PASSWORD: ${{ secrets.ACR_PASSWORD }}
```
