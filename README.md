Overview

This repository contains the application source code for a cloud-native microservices platform deployed on Amazon EKS using GitOps principles.

The platform consists of multiple Java Spring Boot microservices packaged as Docker containers and deployed through a fully automated CI/CD pipeline using GitHub Actions, Amazon ECR, ArgoCD, Helm, and Argo Rollouts.

The application demonstrates modern platform engineering practices including:

Containerized microservices GitOps deployments Progressive delivery Canary deployments Blue/Green deployments Horizontal Pod Autoscaling Observability with OpenTelemetry Amazon EKS workloads running on Karpenter-provisioned nodes

Architecture
```
Developer Commit
        │
        ▼
GitHub Actions
        │
        ▼
Docker Build
        │
        ▼
Amazon ECR
        │
        ▼
GitOps Repository Update
        │
        ▼
ArgoCD Sync
        │
        ▼
Amazon EKS
        │
        ▼
Argo Rollouts
        │
 ┌──────┴──────┐
 │             │
Canary     Blue/Green
Deployments Deployments
```
Microservices

The application consists of the following services:

Service	Description
UI	Frontend retail storefront
Catalog	Product catalog service
Cart	Shopping cart service
Checkout	Checkout workflow service
Orders	Order management service

# CI/CD Pipeline

GitHub Actions automates the application delivery workflow:

Pipeline Stages
1. Build Java application
2. Execute Maven packaging
3. Build Docker image
4. Push image to Amazon ECR
5. Update Helm values with image tag
6. Commit image update to GitOps repository
7. ArgoCD detects change
8. Deploy to Amazon EKS

Example image tags:

sha-fa7dd2d
sha-d01d139
Progressive Delivery
Canary Deployments

Implemented using Argo Rollouts.

Traffic is gradually shifted to the new version:

25%
50%
75%
100%

Benefits:

* Reduced deployment risk
* Early issue detection
* Controlled traffic exposure
  
# Blue/Green Deployments

Implemented using:

ui-active
ui-preview

services.
```
Deployment flow:

Current Version (Blue)
        │
        ▼
Deploy Green Environment
        │
        ▼
Validate Preview
        │
        ▼
Manual Promotion
        │
        ▼
Traffic Switch
        │
        ▼
Scale Down Previous Version
```

This enables zero-downtime application releases.

# Containerization

Each microservice is packaged as a Docker image using multi-stage builds.

Benefits:

* Smaller runtime images
* Reduced attack surface
* Faster deployments
* Separation of build and runtime dependencies

Example:

FROM amazonlinux:2023 AS build-env

# Build application

FROM amazonlinux:2023

# Runtime image only

# Scaling

Horizontal Pod Autoscaler (HPA) automatically scales workloads based on:

* CPU utilization
* Memory utilization

Example configuration:

Min Replicas: 2
Max Replicas: 12
CPU Target: 70%
Memory Target: 80%

# Observability

The platform supports:

Metrics
* OpenTelemetry
* Prometheus
* Grafana
* Tracing
* AWS Distro for OpenTelemetry (ADOT)
* Distributed request tracing

Example dashboards include:

* Cluster utilization
* Pod metrics
* Node metrics
* Network throughput
* Resource consumption
* 
# Running Locally
# Build Application
./mvnw clean package
# Build Docker Image
docker build -t tcollins520/retail-store-ui:latest .
# Run Container
docker run -p 8080:8080 retail-store-ui:latest
# Screenshots
Retail Store UI
* V1 Deployment
* V2 Deployment
* V3 Deployment
# ArgoCD
* Application Topology
* GitOps Synchronization
# Argo Rollouts
* Canary Deployments
* Blue/Green Deployments
# Observability
* Grafana Dashboards
* OpenTelemetry Metrics
* OpenTelemetry Traces
# Technology Stack
Application
* Java 21
* Spring Boot
* Maven
# Containers
* Docker
* Amazon ECR
# Kubernetes
* Amazon EKS
* Helm
* ArgoCD
* Argo Rollouts
* Karpenter
* HPA
# Observability
* OpenTelemetry
* ADOT
* Prometheus
* Grafana
# CI/CD
* GitHub Actions
* GitOps
# Key Skills Demonstrated
* Cloud-Native Architecture
* Microservices
* Containerization
* Kubernetes Operations
* GitOps
* CI/CD Automation
* Progressive Delivery
* Canary Releases
* Blue/Green Deployments
* Platform Engineering
* Observability
* Infrastructure Automation
