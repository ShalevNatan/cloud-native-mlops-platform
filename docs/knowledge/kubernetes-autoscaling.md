# Kubernetes Autoscaling

Kubernetes autoscaling operates at different layers. The two main
mechanisms relevant to this project are HPA and Karpenter.

## HPA — Pod Autoscaling

**Horizontal Pod Autoscaler (HPA)** automatically changes the number
of Pods running for a workload such as a Deployment or StatefulSet.

It can scale based on:

- CPU / memory
- Custom metrics
- External metrics

Basic flow:

    Workload demand
        ↓
    Metrics
        ↓
    HPA
        ↓
    More / fewer Pods

HPA is **reactive**, not predictive. It observes current metrics and
adjusts the replica count accordingly. It does not natively forecast
future demand.

---

## Karpenter — Node Autoscaling

**Karpenter** manages the cluster's compute capacity by dynamically
provisioning and removing Kubernetes nodes.

It observes the requirements of **unscheduled Pods** and determines
what node capacity can satisfy them, while considering constraints
such as CPU, memory, architecture, instance types, zones, and
capacity type.

Basic flow:

    More Pods required
        ↓
    Pod cannot fit on existing nodes
        ↓
    Pod becomes unschedulable
        ↓
    Karpenter
        ↓
    Appropriate node is provisioned
        ↓
    Pod gets scheduled

### "Just-in-time"

"Just-in-time" means Karpenter provisions capacity **when it is
needed**, instead of keeping unnecessary capacity running in advance.

It does **not** mean that Karpenter predicts future workloads.

Karpenter is therefore **reactive**.

Karpenter can also consolidate/remove nodes when existing capacity
is no longer needed, helping reduce infrastructure cost.

---

## HPA vs Karpenter

| | HPA | Karpenter |
|---|---|---|
| Scales | Pods | Nodes |
| Main trigger | Workload metrics | Unscheduled Pods |
| Predicts demand? | No | No |
| Purpose | Match application capacity to demand | Match cluster capacity to Pod requirements |

They work together:

    Demand increases
          ↓
        HPA
          ↓
    More Pods requested
          ↓
    Scheduler tries to place them
          ↓
    Insufficient node capacity
          ↓
      Karpenter
          ↓
    New node provisioned
          ↓
    Pods scheduled

### Key distinction

**HPA answers:**  
"How many Pods should my application have?"

**Karpenter answers:**  
"What compute capacity does the cluster need to run those Pods?"

Neither one is a workload forecasting system.

---

## Next Investigation

- AWS Predictive Scaling
- EKS Auto Mode
- AWS/Kubernetes proactive scaling capabilities
- Whether there is a meaningful ML/MLOps problem beyond the
  capabilities already provided by AWS and Kubernetes
