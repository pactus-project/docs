---
title: Run Pactus Metrics
weight: 9
---

## Preface

Pactus can be run with metrics, providing you with the ability to monitor your node.
This tutorial will guide you through the steps to run Pactus with metrics, suitable for advanced users.

## Prerequisites

Before proceeding with the steps below, ensure that you have the following:

- An understanding of [Prometheus](https://prometheus.io) and [Grafana](https://grafana.com/).
- Have a running Pactus Node.

## Configure Pactus Node for Metrics

To configure the Pactus node for metrics, navigate to the Pactus directory. By default, it’s located at:

```text
/home/YourUsername/pactus
```

There’s a file named `config.toml` that contains all the configurations for your node.
Enable two parameters for metrics: `enable_metrics` and `http.enable`.
After editing `config.toml`, restart your node.
Metrics are available at `http://localhost:80/metrics/prometheus` (this URL will be used by Prometheus).

{{< callout type="info" >}}

If you are running Pactus with the Docker image, make sure to expose port 80.

{{< /callout >}}

---

## Configure Grafana And Prometheus

You should run Grafana and Prometheus for gathering metrics and displaying them in charts.
First, create a directory named `prometheus-grafana`. Inside the directory,
create a `docker-compose.yml` file and paste the code below.

```yaml
services:
  prometheus:
    image: prom/prometheus
    container_name: prometheus
    command:
      - "--config.file=/etc/prometheus/prometheus.yml"
    ports:
      - 9090:9090
    restart: unless-stopped
    volumes:
      - ./prometheus:/etc/prometheus
      - prom_data:/prometheus
  grafana:
    image: grafana/grafana
    container_name: grafana
    ports:
      - 3000:3000
    restart: unless-stopped
    environment:
      - GF_SECURITY_ADMIN_USER=admin
      - GF_SECURITY_ADMIN_PASSWORD=admin
    volumes:
      - ./grafana:/etc/grafana/provisioning/datasources
volumes: prom_data
```

You can change the default username and password of Grafana by modifying the values of `GF_SECURITY_ADMIN_USER` and `GF_SECURITY_ADMIN_PASSWORD`.
Save the file. From the same `prometheus-grafana` directory, create a `grafana` directory and enter it (`/prometheus-grafana/grafana/`).
In that directory, create a file named `datasource.yml` and paste the code below.

```yaml
apiVersion: 1

datasources:
  - name: Prometheus
    type: prometheus
    url: http://prometheus:9090
    isDefault: true
    access: proxy
    editable: true
```

Save the file and exit.
Go up one directory level back to `/prometheus-grafana`.
Create a `prometheus` directory, enter it, and create a file named `prometheus.yml` with the content below.

```yaml
global:
  scrape_interval: 15s
  scrape_timeout: 10s
  evaluation_interval: 15s
alerting:
  alertmanagers:
    - static_configs:
        - targets: []
      scheme: http
      timeout: 10s
      api_version: v1
scrape_configs:
  - job_name: prometheus
    honor_timestamps: true
    scrape_interval: 15s
    scrape_timeout: 10s
    metrics_path: /metrics/prometheus
    scheme: http
    static_configs:
      - targets:
          - 127.0.0.1
```

Then save the file and exit.

{{< callout type="info" >}}

Tip: In the last section of the code, you will see the targets section where 127.0.0.1 is set.
You can change it based on your localhost IP or your domain.
Please ensure that your target matches your node's HTTP port.
The default HTTP port of a Pactus node is 80.

{{< /callout >}}

## Run Grafana and Prometheus

Go to the `/prometheus-grafana` directory where the `docker-compose.yml` is located and run the command below.

```shell
docker compose up -d
```

Congratulations! Grafana and Prometheus are now up and accessible at ports `3000` and `9090` respectively.

## Import Pactus Metrics to Grafana Dashboard

As Pactus uses `libp2p` for its peer-to-peer network, we should import `libp2p` metrics that you can find [here](https://github.com/libp2p/go-libp2p/tree/master/dashboards).
Download one of the metrics config and then Import it into `Grafana Dashboard`.

Congratulations! You did it. Now, you can perform the same operations for other configurations.
