---
title: Access And Ingress
slug: access-and-ingress
---
The cluster is exposed through k3s's built-in Traefik ingress controller and local `.lan` hostnames.

## Local Access Setup

To reach the cluster from another machine on the LAN, point the relevant hostnames at the mini-server IP.

Use either:

- explicit DNS records like `home.lan -> 192.168.1.173`
- or explicit `/etc/hosts` entries for each hostname you want to expose

Do not rely on wildcard `/etc/hosts` entries; hosts files do not support them.

## Ingress Controller

- Controller: `traefik`
- Namespace: `kube-system`
- Service type: `LoadBalancer`
- Purpose: route all browser-facing apps behind a single entry point

## Common Endpoints

| Host | Service |
| --- | --- |
| `home.lan` | Cluster Home |
| `argocd.lan` | ArgoCD |
| `wiki.lan` | Cluster Lite Wiki |
| `gatus.lan` | Gatus status page |
| `jellyfin.lan` | Jellyfin |
| `chat.lan` | Open WebUI |
| `prometheus.lan` | Prometheus UI |
| `grafana.lan` | Grafana |

## Internal Service Pattern

External requests terminate at Traefik, then route to namespace-local ClusterIP services. Internal service-to-service traffic stays on cluster DNS names such as:

- `prometheus-server.monitoring.svc.cluster.local`
- `loki.monitoring.svc.cluster.local`
- `cluster-home.services.svc.cluster.local`
- `grafana.monitoring.svc.cluster.local`
- `argocd-server.argocd.svc.cluster.local`
- `ollama-external.ai.svc.cluster.local`

This keeps public access simple while allowing internal dependencies to use stable service discovery.
