---
title: "Writing Policies"
linkTitle: "Writing Policies"
weight: 2
description: >
  
---

{{% pageinfo %}}

{{% /pageinfo %}}

# Writing Policies

The following picture shows the structure of a Kyverno Policy:

![KyvernoPolicy](https://raw.githubusercontent.com/nirmata/kyverno/master/documentation/assets/images//Kyverno-Policy-Structure.png)

Each Kyverno policy contains one or more rules. Each rule has a `match` clause, an optional `exclude` clause, and one of a `mutate`, `validate`, or `generate` clause.

Each rule can validate, mutate, or generate configurations of matching resources. A rule definition can contain only a single **mutate**, **validate**, or **generate** child node. 

These actions are applied to the resource in described order: mutation, validation and then generation.