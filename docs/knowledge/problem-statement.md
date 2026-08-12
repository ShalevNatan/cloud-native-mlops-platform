# Problem Statement

## Background

During my work with Kubernetes in an on-prem production environment,
I observed that reactive autoscaling can introduce a scaling delay
when workload demand increases rapidly.

## Problem

When demand increases faster than the infrastructure can provision
additional capacity, applications may experience increased latency
or other performance degradation while new Pods and nodes become
available.

## Hypothesis

Application-level ML forecasting may provide advance warning of
predictable or gradually developing workload spikes, allowing
capacity to be provisioned proactively.

## Research Question

Can ML-based application demand forecasting improve Kubernetes
autoscaling enough to reduce performance degradation without causing
unnecessary infrastructure cost?

## Scope

The project will focus on predictable and gradually developing
workload spikes. Reactive autoscaling will remain available as a
fallback for unexpected demand.

## Success Criteria

The predictive approach will be compared against reactive
autoscaling using metrics such as:

- application latency
- scaling response time
- Pending Pods
- resource utilization
- infrastructure cost
- forecast accuracy
