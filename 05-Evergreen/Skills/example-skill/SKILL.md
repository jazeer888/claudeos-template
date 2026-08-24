---
name: example-skill
description: TODO — one sentence describing when Claude should trigger this skill.
---

# example-skill

TODO: instructions, examples, and reference material for this skill.
Delete or rename this folder as your first real skill.

---

## Example (fictional — developer perspective)

If this were a real skill, e.g. `k8s-cost-review`:

```markdown
---
name: k8s-cost-review
description: Use when reviewing Kubernetes manifests or Helm charts for cost
  and resource-efficiency issues — oversized requests/limits, missing
  autoscaling, orphaned PVCs.
---

# k8s-cost-review

Checklist Claude should walk through:
1. Are requests/limits set on every container? Flag anything unset.
2. Compare requested CPU/memory against actual usage (from metrics-server or
   Prometheus) if available — flag >2x over-provisioning.
3. Check for HPA/VPA on anything with variable load.
4. Flag PVCs with no owning workload (likely orphaned from a deleted deploy).

Trigger phrases: "review this deployment for cost", "check resource limits",
"cost audit this manifest".
```
