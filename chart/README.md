## Helm Install

```bash
helm repo add k8s-ephemeral-storage-metrics https://jmcgrath207.github.io/k8s-ephemeral-storage-metrics/chart
helm repo update
helm upgrade --install my-deployment k8s-ephemeral-storage-metrics/k8s-ephemeral-storage-metrics
```

## Values

| Key | Type | Default | Description |
|-----|------|---------|-------------|
| affinity | object | `{}` |  |
| deploy_type | string | `"Deployment"` | Set as Deployment for single controller to query all nodes or Daemonset |
| dev | object | `{"enabled":false,"image":{"imagePullPolicy":"IfNotPresent"}}` | For local development of kind and/or deploy grow and shrink test pods |
| image.imagePullPolicy | string | `"IfNotPresent"` |  |
| image.repository | string | `"ghcr.io/jmcgrath207/k8s-ephemeral-storage-metrics"` |  |
| image.tag | string | `"1.4.3"` |  |
| interval | int | `15` | Polling node rate for exporter |
| log_level | string | `"info"` |  |
| max_node_concurrency | int | `10` | Max number of concurrent query requests to the kubernetes API. |
| metrics | object | `{"adjusted_polling_rate":false,"ephemeral_storage_container_limit_percentage":true,"ephemeral_storage_node_available":true,"ephemeral_storage_node_capacity":true,"ephemeral_storage_node_percentage":true,"ephemeral_storage_pod_usage":true}` | Set metrics you want to enable |
| metrics.adjusted_polling_rate | bool | `false` | Create the ephemeral_storage_adjusted_polling_rate metrics to report Adjusted Poll Rate in milliseconds. Typically used for testing. |
| metrics.ephemeral_storage_container_limit_percentage | bool | `true` | Percentage of ephemeral storage used by a container in a pod |
| metrics.ephemeral_storage_node_available | bool | `true` | Available ephemeral storage for a node |
| metrics.ephemeral_storage_node_capacity | bool | `true` | Capacity of ephemeral storage for a node |
| metrics.ephemeral_storage_node_percentage | bool | `true` | Percentage of ephemeral storage used on a node |
| metrics.ephemeral_storage_pod_usage | bool | `true` | Current ephemeral byte usage of pod |
| nodeSelector | object | `{}` |  |
| podAnnotations | object | `{}` |  |
| prometheus.enable | bool | `true` |  |
| prometheus.release | string | `"kube-prometheus-stack"` |  |
| tolerations | list | `[]` |  |

## Contribute

### Start Kind
```bash
make new_kind
```

### Run locally
```bash
make deploy_local
```

### Run locally with Delve Debug
```bash
make deploy_debug
```
Then connect to `localhost:30002` with [delve](https://github.com/go-delve/delve) or your IDE.

### Run e2e Test
```bash
make deploy_e2e
```

### Debug e2e
```bash
make deploy_e2e_debug
```
Then run a debug against [deployment_test.go](tests/e2e/deployment_test.go)

## License

This project is licensed under the [MIT License](https://opensource.org/licenses/MIT). See the `LICENSE` file for more details.