# Cloud-Native MLOps Platform

A production-oriented cloud-native platform for running machine learning workloads on Kubernetes and AWS.

The project focuses on the **platform engineering side of MLOps**: providing ML engineers and data scientists with reproducible infrastructure and self-service capabilities for training, experimenting with, and deploying machine learning workloads.

The goal is not to develop an ML model ourselves, but to build the platform that enables other engineers and ML specialists to do so reliably.

## Problem

ML teams need more than a Python environment to build and operate machine learning systems.

Training and inference workloads require compute, storage, networking, security, reproducibility, deployment automation, observability, and resource management. Without a dedicated platform, ML engineers may need to manually manage infrastructure and Kubernetes resources for every workload.

This project explores how a cloud-native platform can abstract that infrastructure while still providing the flexibility and control required for real ML workloads.

## Goals

* Build reproducible AWS infrastructure using Infrastructure as Code.
* Provide a Kubernetes-based platform for ML training and inference workloads.
* Allow ML engineers to run workloads without manually managing the underlying cloud infrastructure.
* Provide reproducible environments for ML workloads through containerization.
* Provide storage for datasets, model artifacts, and experiment outputs.
* Automate application and ML workload delivery through CI/CD and GitOps practices where they provide clear value.
* Support experiment tracking and model lifecycle management where required.
* Provide observability for both platform infrastructure and ML workloads.
* Support appropriate compute provisioning and resource management for variable ML workloads.
* Apply practical security, scalability, reliability, and cost-management principles.
* Demonstrate the engineering tradeoffs involved in building and operating an ML platform on AWS and Kubernetes.

## Architecture

The platform is built around Kubernetes running on AWS.

At a high level:

```text
ML Engineer
     │
     ▼
ML Workload
     │
     ▼
┌─────────────────────────────────────┐
│          ML Platform                │
│                                     │
│  Kubernetes / EKS                   │
│  Compute & Scheduling               │
│  Storage & Artifacts                │
│  Workload Execution                 │
│  Experiment Management              │
│  Model Deployment                   │
│  Observability                      │
│  Security & Access Control          │
└──────────────────┬──────────────────┘
                   │
                   ▼
              AWS Services
```

The exact platform components will be selected based on the problems they solve rather than added simply because they are commonly used in MLOps architectures.

## Technology

The project is expected to use technologies from the following areas:

* **AWS** — cloud infrastructure
* **Terraform** — Infrastructure as Code
* **Amazon EKS / Kubernetes** — workload orchestration
* **Amazon ECR** — container image storage
* **Amazon S3** — datasets and artifacts
* **GitHub Actions** — CI/CD
* **GitOps tooling** — declarative workload delivery where justified
* **ML experiment/model management** — where justified by the platform requirements
* **Prometheus / Grafana or equivalent** — observability where justified

The final technology stack is intentionally not fixed in advance. Each major component should have a clear engineering justification.

## Engineering Principles

This project is designed as an engineering project rather than a collection of tools.

Key principles:

1. **Problem before technology**
   Every major component must solve a clearly defined problem.

2. **Reproducibility**
   Infrastructure and workloads should be reproducible from version-controlled definitions.

3. **Automation**
   Repetitive infrastructure and deployment operations should be automated.

4. **Observability**
   Platform behavior should be measurable rather than assumed.

5. **Security by design**
   IAM, Kubernetes access, networking, secrets, and workload permissions should follow least-privilege principles.

6. **Cost awareness**
   Cloud resources should be intentionally sized, monitored, and cleaned up.

7. **Measured decisions**
   Architectural decisions should be supported by experiments, measurements, and documented tradeoffs.

8. **Operational realism**
   The platform should demonstrate how these systems behave under failure, scaling, and changing workload conditions.

## Project Structure

```text
.
├── README.md
├── PROJECT.md
├── ARCHITECTURE.md
├── DECISIONS.md
├── ROADMAP.md
└── docs/
    └── knowledge/
```

The repository documentation is the authoritative source for project decisions and architectural direction.

## Current Status

The project is currently in the **platform and problem-definition phase**.

Initial research has been completed around:

* Kubernetes autoscaling
* HPA
* Karpenter
* AWS autoscaling capabilities
* AWS EC2 Predictive Scaling
* EKS Auto Mode
* Kubernetes application-level metrics
* The original predictive-autoscaling research hypothesis

The project direction is now being evaluated from a broader **ML platform engineering / MLOps** perspective before infrastructure implementation begins.

No AWS infrastructure has been provisioned yet.

## Future Direction

The next phase is to define the platform's target users, core ML workflow, and the specific operational problems the platform should solve.

Only after those requirements are established will the infrastructure and technology choices be finalized.
