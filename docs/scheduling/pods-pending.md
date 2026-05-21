# Diagnosing Kubernetes Pods Pending

## Overview

Pods remaining in `Pending` state usually indicate scheduling or infrastructure constraints.

Common causes include:
- insufficient CPU or memory,
- taints and tolerations mismatch,
- affinity rules,
- storage problems,
- autoscaler issues,
- node selector mismatch.

This document provides a practical troubleshooting workflow.

---

# 1. Check Pod Events

Start by describing the pod:

```bash
kubectl describe pod <pod-name> -n <namespace>
```

Focus on:
- `FailedScheduling`
- volume errors
- taint mismatch
- affinity failures

Example:

```text
0/3 nodes are available: 3 Insufficient memory.
```

---

# 2. Check Cluster Events

Cluster-wide events often reveal scheduling problems.

```bash
kubectl get events -A --sort-by=.lastTimestamp
```

Useful for:
- scheduler failures,
- autoscaler issues,
- storage problems,
- CSI errors.

---

# 3. Check Node Resources

Inspect node utilization:

```bash
kubectl top nodes
```

Then inspect allocatable resources:

```bash
kubectl describe node <node-name>
```

Common issues:
- CPU exhaustion,
- memory exhaustion,
- max pod density reached.

---

# 4. Verify Taints and Tolerations

Inspect node taints:

```bash
kubectl describe nodes | grep Taints
```

Inspect pod tolerations:

```bash
kubectl get pod <pod-name> -n <namespace> -o yaml
```

Typical issue:

```text
node(s) had untolerated taint
```

---

# 5. Verify Affinity Rules

Inspect:
- `nodeSelector`
- `nodeAffinity`
- `podAffinity`
- `podAntiAffinity`

Common issue:
- target labels do not exist on nodes.

Useful command:

```bash
kubectl get nodes --show-labels
```

---

# 6. Check Storage Constraints

Inspect PVC status:

```bash
kubectl get pvc -A
```

Typical storage-related causes:
- StorageClass mismatch,
- unavailable CSI driver,
- zone mismatch,
- stuck volume attachments.

---

# 7. Check Autoscaler or Karpenter

If using autoscaling, inspect autoscaler logs.

Example:

```bash
kubectl logs -n kube-system deployment/karpenter
```

Potential issues:
- instance type restrictions,
- subnet exhaustion,
- IAM permissions,
- NodePool limits.

---

# Troubleshooting Philosophy

Avoid random configuration changes.

Use a structured approach:
1. inspect events,
2. inspect scheduler feedback,
3. inspect nodes,
4. inspect storage,
5. inspect autoscaler behavior.

Most root causes appear in Kubernetes events.
