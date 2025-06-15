# Example API Helm Chart

A Helm chart for deploying a FastAPI Example API to Kubernetes.

## Prerequisites

- Kubernetes cluster (1.19+)
- Helm 3.x
- kubectl configured to access your cluster

## Quick Start

```bash
# Install the chart
helm install example-api .

# Check the deployment
kubectl get pods
kubectl get services
```

## Configuration

Key configurable parameters:

| Parameter | Description | Default |
|-----------|-------------|---------|
| `image.repository` | Container image repository | `mlog/example-api` |
| `image.tag` | Container image tag | `latest` |
| `replicaCount` | Number of replicas | `4` |
| `service.type` | Service type | `LoadBalancer` |
| `service.port` | Service port | `80` |
| `service.targetPort` | Container port | `8000` |
| `autoscaling.enabled` | Enable HPA | `true` |
| `autoscaling.minReplicas` | Min replicas | `2` |
| `autoscaling.maxReplicas` | Max replicas | `6` |

## Installation

```bash
# Install with default values
helm install example-api .

# Install with custom image tag
helm install example-api . --set image.tag=v1.0.0

# Install with custom replica count
helm install example-api . --set replicaCount=2
```

## Health Checks

The API includes health checks at `/health` endpoint:
- Liveness probe: checks every 20s after 15s delay
- Readiness probe: checks every 10s after 5s delay

## Scaling

Horizontal Pod Autoscaler is enabled by default:
- Scales between 2-6 replicas based on CPU usage (80% target)
- Manual scaling: `kubectl scale deployment example-api --replicas=3`

## Upgrading

```bash
helm upgrade example-api .
```

## Uninstalling

```bash
helm uninstall example-api
```

## Development

```bash
# Validate the chart
helm lint .

# Preview templates
helm template example-api .

# Dry run
helm install example-api . --dry-run
```

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.
