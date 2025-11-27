# Mern-Stack-Project
This project implements a complete production-grade DevSecOps pipeline for deploying a three-tier application (database, backend, frontend) on AWS EKS. It integrates Infrastructure as Code, secure CI/CD, GitOps, container security, and full monitoring to demonstrate modern DevOps and Kubernetes practices.
End-to-End DevSecOps Kubernetes Three-Tier Application
Terraform | AWS EKS | Jenkins | ArgoCD | SonarQube | OWASP | Trivy | Prometheus | Grafana

This project demonstrates a complete production-style DevSecOps pipeline deployed on AWS EKS, integrating modern CI/CD automation, GitOps, Infrastructure as Code, and security scanning across every stage of the software delivery lifecycle.

It covers the full workflow from infrastructure provisioning → CI pipeline → GitOps delivery → monitoring → security.
=======================================
🚀 Architecture Overview

This project deploys a three-tier application (DB → Backend → Frontend) running on Amazon Elastic Kubernetes Service (EKS).
The complete workflow includes:

Terraform for provisioning Jenkins server and supporting AWS resources

Jenkins CI for:

Code checkout

SonarQube (SAST)

OWASP Dependency Check (SCA)

Docker image build

Trivy image scan (container security)

Push to private Amazon ECR

Auto-update Kubernetes manifests

ArgoCD GitOps for automated deployment to EKS

AWS Load Balancer Controller for ingress & ALB creation

Prometheus + Grafana for cluster & application monitoring

Persistent Volumes for database durability

Custom DNS mapped to ALB for domain access
============================
🧱 Tech Stack Used
Cloud & IaC

AWS (EKS, ECR, EC2, IAM, ALB, VPC)

Terraform

eksctl

AWS CLI

CI/CD & GitOps

Jenkins

ArgoCD

DevSecOps Tools

SonarQube (Static Code Analysis)

OWASP Dependency-Check (Vulnerability scanning)

Trivy (Container image scanning)

Containers & K8s

Docker

Kubernetes (Deployments, Services, Ingress, PV/PVC)

AWS Load Balancer Controller

Monitoring

Prometheus

Grafana (K8s dashboard ID 6417)
===========================
📦 Pipeline Flow (End-to-End)
1️⃣ Infrastructure Provisioning

IAM user created with programmatic access

Terraform provisions:

Jenkins EC2 instance

S3 backend (optional)

Networking components

eksctl creates:

EKS cluster

Worker nodes

OIDC provider & IAM roles

ALB controller installed via Helm
=========================
2️⃣ CI Pipeline (Jenkins)

Two pipelines: frontend & backend

Stages included:

Checkout code from GitHub

SonarQube analysis → quality gates

OWASP Dependency Check

Install dependencies & run tests

Build Docker image

Trivy image scan

Authenticate & push to private Amazon ECR

Auto-update Kubernetes deployment manifest with new image tag

Commit manifest changes back to Git repo
================================
3️⃣ CD Pipeline (ArgoCD GitOps)

ArgoCD watches Kubernetes manifests repo

Auto-sync enabled for:

Database

Backend

Frontend

Ingress

Any manifest update in GitHub → instantly reflected in EKS

Ensures secure, version-controlled deployments
=======================
4️⃣ Ingress & DNS

Ingress creates AWS Application Load Balancer via ALB Controller

DNS provider maps subdomain → ALB

Application accessible using a friendly URL
==========================
5️⃣ Monitoring Setup

Prometheus installed using Helm

Grafana installed using Helm

Prometheus added as datasource

Imported Kubernetes monitoring dashboard (ID: 6417)

Visualised:

Nodes

Namespaces

Pods

Deployments

Resource usage
=========================
🗄️ Three-Tier Application Components

Database: MongoDB with PersistentVolumeClaim

Backend: NodeJS (Express)

Frontend: ReactJS

Deployed across a dedicated namespace: three-tier
====================
🔐 Security Highlights (DevSecOps)

SAST: SonarQube

SCA: OWASP Dependency Check

Container Scanning: Trivy

Private Images: Amazon ECR

Secret Management: Kubernetes imagePullSecret

Secure CI credentials: Jenkins credential store

GitOps: ArgoCD ensures controlled deploys
====================
🏆 Key Outcomes

Fully automated CI/CD using Jenkins + ArgoCD

GitOps-driven deployments to EKS

A secure pipeline with end-to-end scanning

Highly observable cluster via Prometheus + Grafana

Real-world three-tier application running on AWS

Production-grade architecture with data persistence
===================
📂 Repository Structure
.
├── jenkins/
│   ├── Jenkinsfile-frontend
│   ├── Jenkinsfile-backend
├── k8s-manifests/
│   ├── backend/
│   ├── frontend/
│   ├── database/
│   ├── ingress/
├── terraform/
│   ├── jenkins-server/
│   ├── variables.tfvars
├── application-code/
│   ├── backend/
│   ├── frontend/
=========================
🧩 How to Reuse This Project

You can extend it by adding:

HPA (Horizontal Pod Autoscaler)

ALB HTTPS SSL termination

Secret Managers (AWS Secrets Manager / HashiCorp Vault)

Logging (EFK / Loki stack)

Karpenter for autoscaling
=============================
⭐ Conclusion

This project demonstrates how to build a secure, fully automated DevSecOps pipeline around a modern Kubernetes architecture using industry-leading tools. It reflects real enterprise workflows including secure CI, GitOps-driven CD, cloud-native deployments, and full observability.
