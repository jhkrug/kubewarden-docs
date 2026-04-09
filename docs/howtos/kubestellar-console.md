---
sidebar_label: KubeStellar Console
sidebar_position: 100
title: Installing Kubewarden with KubeStellar Console
description: How to install Kubewarden using the KubeStellar Console guided install mission.
keywords: [kubewarden, kubernetes, kubestellar, console, guided install]
doc-persona: [kubewarden-operator, kubewarden-integrator]
doc-type: [howto]
doc-topic: [kubestellar-console-installation]
---

<head>
  <link rel="canonical" href="https://docs.kubewarden.io/howtos/kubestellar-console"/>
</head>

[KubeStellar Console](https://console.kubestellar.io) is a standalone
Kubernetes dashboard that includes guided install missions for CNCF projects.
The Kubewarden install mission walks you through the full installation
step-by-step, with live cluster validation after each step.

## What the mission does

The guided install mission runs against your cluster via kubeconfig. Each step:

1. **Pre-flight** -- checks prerequisites (Helm 3, kubectl, cluster access)
2. **Commands** -- shows the exact `helm install` commands for all three charts
   (`kubewarden-crds`, `kubewarden-controller`, `kubewarden-defaults`) with
   `--wait` flags, matching the
   [quick-start](https://docs.kubewarden.io/quick-start) docs
3. **Validation** -- after each step, queries the cluster to verify success
   (pod phase, PolicyServer registration)
4. **Troubleshooting** -- on failure, reads pod logs, events, and resource
   status from your cluster and suggests fixes
5. **Rollback** -- each step includes the corresponding `helm uninstall` command
   to undo the change

The mission also works as read-only documentation -- no cluster connection is
required to browse the steps.

## Prerequisites

- A running Kubernetes cluster
- `kubectl` configured with access to the cluster
- [Helm](https://helm.sh/) v3 installed
- [KubeStellar Console](https://console.kubestellar.io) installed
  (see the [install guide](https://github.com/kubestellar/console#install) for
  options including Homebrew, Docker, and binary downloads)

## Opening the install mission

1. Launch KubeStellar Console and connect to your cluster.
2. Open the **AI Mission Explorer** from the sidebar.
3. Search for **Kubewarden** or browse the **Install** category.
4. Select the **Install Kubewarden** mission to begin.

Alternatively, open the mission directly at:

```text
https://console.kubestellar.io/missions/install-kubewarden
```

## Installation steps

The mission guides you through the following Helm chart installations in order:

### 1. Install CRDs

```console
helm repo add kubewarden https://charts.kubewarden.io
helm repo update kubewarden
helm install --wait \
  -n kubewarden \
  --create-namespace \
  kubewarden-crds kubewarden/kubewarden-crds
```

The mission validates that the Kubewarden CRDs are registered in the cluster
before proceeding.

### 2. Install the controller

```console
helm install --wait \
  -n kubewarden \
  kubewarden-controller kubewarden/kubewarden-controller
```

The mission validates that the controller pod reaches `Running` status.

### 3. Install defaults

```console
helm install --wait \
  -n kubewarden \
  kubewarden-defaults kubewarden/kubewarden-defaults
```

The mission validates that the default `PolicyServer` is registered and ready.

## What's next

After completing the mission, you have a working Kubewarden installation with
the default PolicyServer. From here you can:

- [Create your first policy](https://docs.kubewarden.io/quick-start#defining-your-first-policy)
- [Explore the policy catalog](https://artifacthub.io/packages/search?kind=13)
- Browse additional install missions for other CNCF projects in the
  [KubeStellar Console mission explorer](https://console.kubestellar.io/missions)

## Resources

- [Mission definition on GitHub](https://github.com/kubestellar/console-kb/blob/master/fixes/cncf-install/install-kubewarden.json)
- [KubeStellar Console](https://console.kubestellar.io)
- [KubeStellar Console on GitHub](https://github.com/kubestellar/console)
