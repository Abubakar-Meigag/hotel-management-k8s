# Hotel Management System — Kubernetes & GitOps

This repository contains all Kubernetes manifests, Istio service mesh configurations, and Argo CD application definitions for deploying the Hotel Management System.

## Application Repository

The main application code lives here:
👉 https://github.com/Abubakar-Meigag/hotel-management-system

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
