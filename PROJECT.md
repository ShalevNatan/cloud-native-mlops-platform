# Project

## Name

Cloud-Native MLOps Platform

## Goal

Investigate whether application-level ML forecasting can improve
Kubernetes autoscaling by providing advance warning of predictable
or gradually developing workload spikes.

## Problem

Reactive autoscaling can introduce a delay between increasing
workload demand and the availability of additional compute capacity.

## Approach

Build an EKS-based Kubernetes environment and compare:

1. Reactive autoscaling using HPA and Karpenter.
2. Predictive scaling using application-level ML forecasting,
   while retaining reactive autoscaling as a fallback.

## Evaluation

The approaches will be compared using:

- Application latency
- Scaling response time
- Pending Pods
- Resource utilization
- Infrastructure cost
- Forecast accuracy

## Scope

The project focuses on predictable and gradually developing workload
spikes. Unexpected spikes remain the responsibility of reactive
autoscaling.
