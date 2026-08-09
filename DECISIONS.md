# Architecture Decisions

## ADR-001 — Use Amazon EKS

### Decision

Use Amazon EKS as the primary Kubernetes platform.

### Reason

The project is intended to demonstrate AWS and Kubernetes
engineering together. EKS provides experience with managed
Kubernetes and AWS-specific integration.

### Alternative Considered

My self-hosted K3s.

### Why K3s Was Not Selected

K3s is useful for lightweight Kubernetes and homelab environments,
but EKS provides greater exposure to AWS networking, IAM,
managed Kubernetes, and cloud-native architecture.

### Status

Accepted
