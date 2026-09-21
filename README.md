# Microservice Deployment of Java Application Using CI/CD

**Tools:** Jenkins · Git · Maven · Docker · Docker Hub · Kubernetes · Prometheus · Grafana

## 📌 Overview

Modernized and automated the deployment of a Java microservice application by implementing an end-to-end CI/CD pipeline. The project automates application build, testing, containerization, Docker image publishing, Kubernetes deployment, and infrastructure monitoring.


##Note: This repo contains source code, dockerfile, Manifest File, Jenkinsfile (containing pipeline script).   

## 🏗️ Architecture

```text
Git Repository
      ↓
Jenkins Controller
      ↓
Jenkins Build Agent
      ↓
Maven Build & Test
      ↓
Docker Build
      ↓
Docker Hub
      ↓
Kubernetes Cluster
 ┌───────────────┐
 │ Control Plane │
 └───────┬───────┘
     ┌───┴───┐
     ↓       ↓
 Worker 1  Worker 2
      ↓
Prometheus → Grafana
```

## 🔄 CI/CD Pipeline

1. **Git Checkout** – Retrieves application source code from the repository.
2. **Build & Test** – Maven compiles the application, runs tests, and generates artifacts.
3. **Docker Build** – Creates a container image using the application Dockerfile.
4. **Docker Hub** – Publishes the container image to Docker Hub.
5. **Kubernetes Deployment** – Jenkins transfers Kubernetes manifests to the control plane and deploys the application across worker nodes.
6. **Monitoring** – Prometheus collects infrastructure metrics and Grafana visualizes them through dashboards.

## ☸️ Infrastructure

* **Jenkins:** 1 Controller + 1 Build Agent
* **Kubernetes:** 1 Control Plane + 2 Worker Nodes
* **Monitoring:** Dedicated Prometheus & Grafana server
* **Deployment:** Jenkins + SSH + Kubernetes manifests

## 🎯 Key Highlights

* Distributed Jenkins CI/CD architecture
* Automated Maven build and testing
* Docker containerization and Docker Hub integration
* Kubernetes-based application deployment
* Automated deployment using Jenkins SSH integration
* Prometheus and Grafana monitoring

## 🛠️ Technologies

`Java` `Git` `Maven` `Jenkins` `Docker` `Docker Hub` `Kubernetes` `kubeadm` `Prometheus` `Grafana` `Linux`

