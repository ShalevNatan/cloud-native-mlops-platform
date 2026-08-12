# AWS Autoscaling

## EC2 Predictive Scaling

EC2 Predictive Scaling uses historical CloudWatch metrics to forecast
future application load and proactively increase capacity in an EC2
Auto Scaling Group.

It needs at least 24 hours of historical data and can analyze up to
14 days to produce an hourly forecast for the next 48 hours. It works
best for recurring and predictable workload patterns. AWS also
supports custom CloudWatch metrics. 

Basic flow:

    Historical CloudWatch data
            ↓
    Predictive Scaling
            ↓
    Forecast future capacity
            ↓
    EC2 Auto Scaling Group
            ↓
    EC2 instances

## EKS Auto Mode

EKS Auto Mode automatically manages parts of the EKS data plane,
including node provisioning and consolidation. Its node provisioning
is Karpenter-based and reacts to Pods that cannot be scheduled on
existing capacity. It does not predict future Kubernetes workload
demand. 

## Why EC2 Predictive Scaling is not enough for our problem

EC2 Predictive Scaling can predict future EC2 capacity requirements,
but our problem is specifically **Kubernetes application demand**.

Karpenter is workload-aware: it looks at unscheduled Pods and their
requirements to determine what node capacity is needed. EC2 Predictive
Scaling forecasts capacity for an Auto Scaling Group instead. 

Even if we publish Kubernetes/application metrics to CloudWatch,
Predictive Scaling would still be forecasting an EC2 Auto Scaling
Group rather than directly making Kubernetes workload decisions.

Therefore, our research question remains:

    Can application-level ML forecasting provide useful advance
    warning of Kubernetes workload spikes and improve the existing
    reactive scaling path?

Predictive scaling and reactive Kubernetes autoscaling are not
mutually exclusive. A predictive layer could potentially prepare
capacity in advance, while HPA/Karpenter remain the safety net for
unexpected demand.
