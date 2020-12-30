---
type: "docs"
title: Disallow Sysctls
linkTitle: Disallow Sysctls
weight: 16
description: >
    The Sysctl interface allows modifications to kernel parameters at runtime. In a Kubernetes pod these parameters can be specified under `securityContext.sysctls`. Kernel parameter modifications can be used for exploits and should be restricted.
---

## Category
Security

## Definition
[/best-practices/disallow_sysctls.yaml](https://github.com/kyverno/policies/raw/main//best-practices/disallow_sysctls.yaml)

```yaml
apiVersion: kyverno.io/v1
kind: ClusterPolicy
metadata:
  name: disallow-sysctls
  annotations:
    policies.kyverno.io/category: Security
    policies.kyverno.io/description: The Sysctl interface allows modifications to kernel parameters 
      at runtime. In a Kubernetes pod these parameters can be specified under `securityContext.sysctls`. 
      Kernel parameter modifications can be used for exploits and should be restricted.
spec:
  validationFailureAction: audit
  rules:
  - name: validate-sysctls
    match:
      resources:
        kinds:
        - Pod
    validate:
      message: "Changes to kernel parameters are not allowed"
      pattern:
        spec:
          =(securityContext):
            X(sysctls): null
```