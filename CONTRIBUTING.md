# Contributing to GPU Usage Monitor

Thank you for your interest in contributing to the GPU Usage Monitor! This project welcomes contributions of new panels and dashboards for GPU monitoring in Kubernetes clusters.

## What You Can Contribute

- **New Panels** - Add visualization panels for GPU metrics (utilization, memory, allocation, etc.)
- **New Dashboards** - Create dashboard layouts combining multiple panels for specific use cases

## Available Metrics

When building panels, you can use metrics from:

- **DCGM Exporter** - GPU metrics like `DCGM_FI_DEV_GPU_UTIL`, `DCGM_FI_DEV_FB_FREE`, `DCGM_FI_DEV_FB_USED`
- **kube-state-metrics** - Kubernetes pod and resource metrics

## How to Contribute

1. **Fork and Clone** - Fork the repository and clone it locally
2. **Create a Branch** - Use a descriptive name like `panel/gpu-temperature` or `dashboard/multi-node-overview`
3. **Develop Your Panel/Dashboard**
   - Create your Grafana dashboard JSON and add it to the `dashboards/` directory
   - Register your dashboard in `templates/grafana/configmap.yaml` by adding an entry:
     ```yaml
     your-dashboard-name.json: |
     {{ .Files.Get "dashboards/your-dashboard-name.json" | indent 4 }}
     ```
4. **Test Locally** - Install the Helm chart and verify your contribution works:
   ```bash
   helm install gpu-usage-monitor . --namespace gpu-usage-monitor --create-namespace
   kubectl port-forward -n gpu-usage-monitor svc/gpu-usage-monitor-grafana 3000:80
   ```
5. **Submit a PR** - Open a pull request with a clear description

## Pull Request Guidelines

- Provide a clear title describing your panel or dashboard
- Include a screenshot showing the visualization
- Describe what metrics are displayed and the use case
- Ensure the dashboard loads correctly with the default Prometheus data source

## Getting Help

If you have questions, open an issue on GitHub.

## License

By contributing, you agree that your contributions will be licensed under the Apache License 2.0.
