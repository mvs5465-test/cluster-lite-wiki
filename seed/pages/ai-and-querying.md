---
title: AI And Querying Stack
slug: ai-and-querying
---
The AI side of the cluster currently exposes a browser chat interface while keeping the older query-router and MCP-facing browser entrypoints disabled.

## Current State

- `chat.lan` is part of the desired live ingress set again
- `info.lan` is still not part of the current desired live ingress set
- the older query-router and MCP-oriented manifests remain in `apps/disabled/` in `local-k8s-apps`

## Open WebUI

The user-facing chat entry point is Open WebUI:

- Service: `open-webui`
- Namespace: `ai`
- Host: `chat.lan`
- Authentication: disabled for local LAN use

Open WebUI connects directly to the cluster-facing Ollama service alias:

- `http://ollama-external.ai.svc.cluster.local:11434`

## Ollama Host

Ollama runs directly on the mini-server host rather than as an in-cluster workload.

- Host machine: `mini-server`
- LAN IP: `192.168.1.173`
- Port: `11434`

The cluster reaches it through the `ollama-external` service in namespace `ai`, which keeps in-cluster clients on stable Kubernetes DNS even though the actual model runtime is host-local.

## Cluster Query Router

`cluster-query-router` is currently kept disabled rather than exposed at `info.lan`.

## MCP Services

| Service | Namespace | Purpose |
| --- | --- | --- |
| Prometheus MCP | `monitoring` | Structured metrics access when enabled |
| Loki MCP | `monitoring` | Structured log access when enabled |

These components are still part of the broader cluster tooling story, but the currently restored browser-facing AI path is Open WebUI plus the mini-server Ollama host.
