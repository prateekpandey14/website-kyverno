---
type: "docs"
title: Restrict External Ips
linkTitle: Restrict External Ips
weight: 29
description: >
    
---

## Category


## Definition
[/other/restrict-service-external-ips.yaml](https://github.com/kyverno/policies/raw/main//other/restrict-service-external-ips.yaml)

```yaml
apiVersion: kyverno.io/v1
kind: ClusterPolicy
metadata:
  name: restrict-external-ips
spec:
  validationFailureAction: audit
  rules:
  - name: check-ips
    match:
      resources:
        kinds:
        - Service
    validate:
      message: "externalIPs are not allowed"
      pattern:
        spec:
          # this prevents any external IP address (see https://github.com/kubernetes/kubernetes/issues/97076#)
          # you can alternatively restrict to a known set of addresses using:
          #     =(externalIPs): ["37.10.11.53", "153.10.20.1"]
          # Note: this currently needs to be an exact ordered set (see https://github.com/kyverno/kyverno/issues/1367).
          X(externalIPs): nil
```