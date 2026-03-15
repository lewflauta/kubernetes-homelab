# ☸️ The Kubernetes Homelab

A streamlined, GitOps-managed Kubernetes cluster running on bare-metal Raspberry pi hardware. This repository serves as the single source of truth for the entire infrastructure.

---

## 🛠 Infrastructure Specifications

### Hardware
3 Raspberry Pi's 2 in kubernetes cluster, 1 Talos
| Component | Specification |
| --- | --- |
| **Systems** | 2x Raspberry Pi 5 |
| **CPU** | 4 Cores per system |
| **RAM** | 8 GB per system |
| **OS** | Raspbian OS |

| **Systems** | Raspberry Pi 5 |
| **CPU** | 4 Cores |
| **RAM** | 8 GB |
| **OS** | Talos OS |

### Software Stack

* **Kubernetes Distribution:** [k3s](https://k3s.io/) (Lightweight K8s)
* **GitOps Tool:** [FluxCD](https://fluxcd.io/)
* **Secret Management:** [Mozilla SOPS](https://github.com/getsops/sops)

---

## 🔌 Networking & Access

The cluster is designed with a "security-first" approach, utilizing a mix of public tunnels and private mesh networking.

* **Local Access:** Accessible via standard local network.
* **Remote Access:** Secured via **Tailscale VPN**.
* **Ingress:** Managed via **Cloudflare Tunnels** for public-facing services.

---

## 🏗 Prerequisites

Ensure you have the following CLI tools installed before interacting with the cluster:

* [flux-cli](https://fluxcd.io/flux/installation/#install-the-flux-cli)
* [kubectl](https://kubernetes.io/docs/tasks/tools/#kubectl)
* [git](https://git-scm.com/downloads)
* [cloudflared](https://developers.cloudflare.com/cloudflare-one/networks/connectors/cloudflare-tunnel/downloads/)
* [sops](https://fluxcd.io/flux/guides/mozilla-sops/)

---

## 🚀 Bootstrap FluxCD

FluxCD automates the deployment of everything in this repo. Follow these steps to initialize the cluster.

### 1. Set Credentials

```bash
export GITHUB_TOKEN=<your-token>
export GITHUB_USER=<your-username>

```

### 2. Verify Environment

```bash
# Install Flux CLI (if using Homebrew)
brew install fluxcd/tap/flux

# Verify cluster compatibility
flux check --pre

```

### 3. Bootstrap Cluster

```bash
flux bootstrap github \
  --owner=$GITHUB_USER \
  --repository=k8s-cluster \
  --branch=main \
  --path=./clusters/staging \
  --personal

```

> [!IMPORTANT]
> After bootstrapping, you must manually create the **SOPS age secret** in the `flux-system` namespace to allow Flux to decrypt your encrypted secrets.

---

## 🌐 Application Endpoints

### Publicly Accessible

| Service | URL |
| --- | --- |
| **Linkding** |  |
| **Nextcloud** |  |

### Internal (VPN Required)

| Service | URL |
| --- | --- |
| **Grafana** |  |

---

