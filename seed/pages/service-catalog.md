---
title: Service Catalog
slug: service-catalog
---
This page is the quick inventory of what is running in the cluster and why.

## Infrastructure And Monitoring

| Service | Namespace | Purpose |
| --- | --- | --- |
| ArgoCD | `argocd` | GitOps deployment control plane |
| External Secrets | `external-secrets` | Syncs secret data into the cluster |
| Grafana Kubernetes Monitoring | `monitoring` | Alloy-managed metrics, events, and log collection |
| Prometheus | `monitoring` | Metrics backend, retention, and query UI |
| Grafana | `monitoring` | Dashboards and visual analysis |
| Loki | `monitoring` | Log aggregation backend |
| Traefik | `kube-system` | Built-in k3s ingress layer for `.lan` routes |

## User-Facing Services

| Service | Namespace | Host | Purpose |
| --- | --- | --- | --- |
| Cluster Home | `services` | `home.lan` | Main custom dashboard with curated links |
| Cluster Lite Wiki | `services` | `wiki.lan` | Lightweight internal docs |
| Gatus | `services` | `gatus.lan` | Uptime checks and status |
| Jellyfin | `services` | `jellyfin.lan` | Media library and streaming |
| ArgoCD | `argocd` | `argocd.lan` | GitOps control plane and app sync status |
| Prometheus | `monitoring` | `prometheus.lan` | Metrics query UI |
| Grafana | `monitoring` | `grafana.lan` | Dashboards and visual analysis |

## AI And Tooling

| Service | Namespace | Host | Purpose |
| --- | --- | --- | --- |
| Chat (Open WebUI) | `ai` | `chat.lan` | Browser chat UI backed by the mini-server Ollama host |
| Ollama External | `ai` | internal | Cluster-facing service alias for the host-level Ollama runtime |
| GitHub PR Slack Notifier | `github-pr-slack-notifier` | internal | Sends Slack notifications for GitHub PR activity |

## Notes

- `Cluster Home` is the primary navigation layer for the local cluster.
- `Cluster Lite Wiki` is optimized for fast browser editing and operational notes.
- Some older app manifests remain in `apps/disabled/`, but this page tracks the current desired live set.
