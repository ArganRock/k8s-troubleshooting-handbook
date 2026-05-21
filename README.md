# Kubernetes Troubleshooting Handbook

Real-world Kubernetes troubleshooting notes, production debugging workflows, and operational knowledge collected from infrastructure and cloud-native environments.

---

# Topics

## Scheduling
- Pods Pending
- Node Affinity
- Taints and Tolerations
- Resource Exhaustion

## Storage
- CSI issues
- PVC Pending
- Longhorn troubleshooting
- Volume attachment failures

## Networking
- DNS
- CoreDNS
- Ingress debugging
- CNI troubleshooting

## GitOps
- ArgoCD
- Drift detection
- Sync failures

## Infrastructure
- EKS
- RKE2
- Karpenter
- High availability concepts

## Security
- RBAC
- Network Policies
- Admission Controllers
- Runtime security

---

# Philosophy

This repository focuses on:
- practical troubleshooting,
- operational thinking,
- root cause analysis,
- production-oriented debugging,
- reliability engineering principles.

The goal is to document real operational patterns and troubleshooting methodologies rather than theoretical examples.

---

# Repository Structure

```text
docs/
├── scheduling/
├── storage/
├── networking/
├── security/
├── gitops/
└── infrastructure/
```

---

# Current Guides

- Diagnosing Kubernetes Pods Pending

---

# Disclaimer

All examples are generalized and sanitized for educational purposes.

No proprietary infrastructure, credentials, customer data, or confidential operational information is included.
