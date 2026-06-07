# Hotel Management System — Kubernetes & GitOps

This repository contains all Kubernetes manifests, Istio service mesh configurations, and Argo CD application definitions for deploying the Hotel Management System.

## Application Repository

The main application code lives here:

👉  https://github.com/Abubakar-Meigag/hotel-management-system

## About the Application

A full microservices-based Hotel Management System built with Java 17+ and Spring Boot. It manages room bookings, guest check-ins/check-outs, housekeeping, billing, and automated notifications.

### Services

| Service | Port | Description |
|---------|------|-------------|
| hotel-api-gateway | 8080 | Single entry point for all requests |
| hotel-room-service | 8081 | Room management |
| hotel-booking-service | 8082 | Bookings and reservations |
| hotel-guest-service | 8083 | Guest accounts |
| hotel-housekeeping-service | 8084 | Housekeeping logs |
| hotel-billing-service | 8085 | Invoices and payments |
| hotel-notification-service | 8086 | Email and SMS alerts |

### Tech Stack

| Layer | Technology |
|-------|------------|
| Language | Java 25 |
| Framework | Spring Boot 4.x |
| Database | PostgreSQL |
| Messaging | RabbitMQ |
| Containerization | Docker |

## About This Repository

This repo follows the GitOps pattern — infrastructure and deployment configuration is stored separately from application code. Any change pushed here is automatically picked up and deployed by Argo CD.

### What This Repo Contains

- `k8s/` — Kubernetes Deployment, Service, ConfigMap and Secret manifests for each microservice
- `istio/` — VirtualService and DestinationRule configs for traffic management and mTLS
- `argocd/` — Argo CD Application definitions

## Prerequisites

- Kubernetes cluster (Minikube for local)
- kubectl installed
- Istio installed
- Argo CD installed

## Folder Structure

```
hotel-management-k8s/
├── k8s/
│   ├── namespace.yaml
│   ├── secrets.yaml
│   ├── configmap.yaml
│   ├── room-service/
│   │   ├── deployment.yaml
│   │   └── service.yaml
│   ├── booking-service/
│   ├── guest-service/
│   ├── housekeeping-service/
│   ├── billing-service/
│   ├── notification-service/
│   └── api-gateway/
├── istio/
│   ├── gateway.yaml
│   └── virtual-services/
└── argocd/
    └── application.yaml
```

## Phase 1 — Kubernetes

**Goal:** Orchestrate the containers using Kubernetes locally with Minikube.

1. Install Minikube and kubectl
2. Create a `Deployment` manifest for each service
3. Create a `Service` manifest for each service to expose ports
4. Create a `ConfigMap` for shared configuration
5. Create a `Secret` for database credentials
6. Deploy all services to Minikube and verify they communicate
7. Set up an Ingress controller to replace the API gateway

---

## Phase 2 — Istio

**Goal:** Add a service mesh for traffic management and security.

1. Install Istio on the Minikube cluster
2. Enable automatic sidecar injection on the hotel namespace
3. Create `VirtualService` and `DestinationRule` for each service
4. Configure mTLS between services
5. Test traffic routing and load balancing
6. Visualize the service mesh using Kiali dashboard

---

## Phase 3 — Argo CD

**Goal:** Set up a GitOps deployment pipeline.

1. Install Argo CD on the Kubernetes cluster
2. Connect Argo CD to the hotel-management-k8s GitHub repository
3. Create an Argo CD Application manifest
4. Configure auto-sync so every git push deploys automatically
5. Test the pipeline by pushing a change and watching it deploy

---

## Phase 4 — Helm

**Goal:** Package Kubernetes manifests into reusable Helm charts.

1. Install Helm locally
2. Create a Helm chart for the hotel services
3. Replace individual deployment and service YAML files with templates
4. Create a values.yaml file for each service
5. Update Argo CD to deploy via Helm charts instead of raw YAML
6. Test deploying a change via Helm and Argo CD together

---

## Phase 5 — Monitoring

**Goal:** Monitor all services with Prometheus and Grafana.

1. Deploy Prometheus to the Kubernetes cluster
2. Configure Spring Boot Actuator endpoints for metrics collection
3. Deploy Grafana and connect it to Prometheus
4. Create dashboards for each service showing request rates and errors
5. Set up alerts for service downtime

---

## Phase 6 — AWS Deployment

**Goal:** Deploy the full system to AWS.

1. Create an EKS cluster on AWS
2. Push all images to AWS ECR
3. Update Kubernetes manifests to use ECR image URLs
4. Configure AWS RDS for PostgreSQL
5. Configure AWS MQ for RabbitMQ
6. Deploy all services to EKS
7. Set up AWS Load Balancer for the API gateway

---

## Phase 7 — GitHub Actions CI/CD

**Goal:** Automate the full deployment pipeline.

1. Create a GitHub Actions workflow in the Java repo
2. On merge to main: run tests, build JAR, build Docker image, push to ECR
3. Automatically update image tag in hotel-management-k8s repo
4. Argo CD picks up the change and deploys automatically
5. Test the full pipeline end to end

---