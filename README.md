# Kubernetes Starter

A beginner-friendly starter repository for setting up local Kubernetes clusters and practicing core Kubernetes manifests.

## Repository Structure

| Path                                                         | Description                                                                                                             |
| ------------------------------------------------------------ | ----------------------------------------------------------------------------------------------------------------------- |
| [`kind/`](./kind/)                                           | Multi-node local cluster setup using **KIND** (Kubernetes in Docker), installer script, and Kubernetes Dashboard setup. |
| [`minikube/`](./minikube/)                                   | Single-node local cluster installation guide for **Minikube** on Ubuntu.                                                |
| [`manifests/`](./manifests/)                                 | Sample Nginx Kubernetes manifests (`Namespace`, `Pod`, `Deployment`, `Service`).                                        |
| [`.github/workflows/lint.yml`](./.github/workflows/lint.yml) | CI checks for shell scripts (`shellcheck`), YAML syntax (`yamllint`), and Kubernetes schemas (`kubeconform`).           |

## Choosing KIND vs. Minikube

| Feature         | KIND                                                          | Minikube                                                                   |
| --------------- | ------------------------------------------------------------- | -------------------------------------------------------------------------- |
| **Topology**    | Multi-node (1 control-plane + 3 workers in `kind-config.yml`) | Single-node by default                                                     |
| **Best for**    | Testing multi-node scheduling, Ingress, and CI-like setups    | Quick single-node learning, built-in addons (`minikube addons`)            |
| **Setup guide** | [`kind/README.md`](./kind/README.md)                          | [`minikube/minikube_installation.md`](./minikube/minikube_installation.md) |

## Quick Start

1. **Create a local cluster** using either:
   - [KIND Setup Guide](./kind/README.md), or
   - [Minikube Installation Guide](./minikube/minikube_installation.md)

2. **Deploy the sample Nginx manifests:**

   ```bash
   kubectl apply -f manifests/namespace.yml
   kubectl apply -f manifests/deployment.yml -f manifests/service.yml
   ```

3. **Access Nginx locally:**

   ```bash
   kubectl -n nginx port-forward svc/nginx-service 8080:80
   ```

   Open `http://localhost:8080` in your browser. See [`manifests/README.md`](./manifests/README.md) for full details on each manifest.
