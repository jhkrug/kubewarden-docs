---
sidebar_label: Capabilities call reference
title: Host capabilities call reference
description: List of all host capabilities calls
keywords:
  [kubewarden, kubernetes, policyserver, host-capabilities,capabilities,namespaced-policies,security]
doc-persona: [kubewarden-operator, kubewarden-integrator]
doc-type: [reference]
doc-topic:
  [
    operator-manual,
    policy-servers,
    host-capabilities,
    namespaced-policies,
    security,
  ]
---

<head>
  
  <link rel="canonical" href="https://docs.kubewarden.io/reference/spec/host-capabilities/call-reference"/>
</head>


Each host capability is identified by a path string. The following paths can
be gated in `spec.namespacedPoliciesCapabilities`:

| Category | Path | Description |
|----------|------|-------------|
| OCI | `oci/v1/verify` | Verify an OCI artifact signature (v1) |
| OCI | `oci/v2/verify` | Verify an OCI artifact signature (v2) |
| OCI | `oci/v1/manifest_digest` | Fetch an OCI manifest digest |
| OCI | `oci/v1/oci_manifest` | Fetch an OCI manifest |
| OCI | `oci/v1/oci_manifest_config` | Fetch an OCI manifest config |
| Kubernetes | `kubernetes/can_i` | Perform a SubjectAccessReview check |
| Net | `net/v1/dns_lookup_host` | Resolve a hostname via DNS |
| Crypto | `crypto/v1/is_certificate_trusted` | Verify certificate trust chain |

:::note
The `kubernetes/list_resources_by_namespace`, `kubernetes/list_resources_all`,
and `kubernetes/get_resource` calls are not applicable to namespaced policies
because those policies have no `spec.contextAwareResources` field. They are
only relevant for `ClusterAdmissionPolicy` resources, which always receive
full host capability access.

The `tracing/log` call emits a log entry and is always available.
:::
