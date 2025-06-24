# Monitoring Stack

This project provides a complete observability stack using **Prometheus**, **Grafana**, **Loki**, **Promtail**, **Alertmanager**, and **Node Exporter** — all orchestrated via Docker Compose.

It enables centralized **metrics collection**, **log aggregation**, and **alerting** for Linux servers in single-node or internal environments.

---

## 🔧 Components

- **Grafana** – A powerful visualization and analytics tool for metrics and logs.
- **Prometheus** – Collects and stores time series metrics.
- **Loki** – A log aggregation system designed to work seamlessly with Grafana.
- **Promtail** – Log collector that ships local logs to Loki.
- **Alertmanager** – Handles alerts from Prometheus and routes them to Mattermost or other systems.
- **Node Exporter** – Exposes system-level metrics (CPU, memory, disk, network, etc.).

---

## 🚀 Getting Started

### 1. Adjust Configuration

Edit the Prometheus targets in `config/prometheus/prometheus.yml` and update IP addresses and labels based on your infrastructure.

### 2. Start the Stack

```bash
USER_ID=$(id -u) docker compose up -d
```

This launches the monitoring stack in the background. The `USER_ID` ensures proper file permissions for the Grafana container.

### 3. Access Grafana

- URL: [http://localhost:3000](http://localhost:3000)
- Default credentials:  
  - **Username:** `admin`  
  - **Password:** `admin`

---

## 🌐 Service URLs

| Service        | URL                             | Description                        |
|----------------|----------------------------------|------------------------------------|
| Grafana        | `http://localhost:3000`          | Dashboards and visualizations      |
| Prometheus     | `http://localhost:9090`          | Query metrics (PromQL)             |
| Alertmanager   | `http://localhost:9093`          | Manage and route alerts            |
| Loki           | `http://localhost:3100/metrics`  | Loki metrics                       |
| Loki Readiness | `http://localhost:3100/ready`    | Health/readiness check             |
| Node Exporter  | `http://localhost:9100/metrics`  | System metrics (host mode)         |

> If running on a remote server, replace `localhost` with the server’s IP address or hostname.

---

## 🧠 Prometheus Configuration

Prometheus config is located in:

```
config/prometheus/prometheus.yml
```

- Scrapes itself, Alertmanager, Loki, and Node Exporters
- Supports multiple environments and datacenters via labels

---

## 📦 Node Exporter

Runs with `host` networking to access system metrics directly.  
Collected metrics include:

- CPU usage
- Memory and swap
- Disk I/O and filesystem stats
- Network statistics

---

## 📊 Create Dashboards in Grafana

1. Add data sources:
   - **Prometheus**: `http://prometheus:9090`
   - **Loki**: `http://loki:3100`

2. Import dashboards:
   - Prometheus Monitoring: Dashboard ID **1860**
   - Loki Logs: Dashboard ID **13639**

3. Or create your own dashboards using PromQL and LogQL.

---

## 📄 License

This project is licensed under the [MIT License](LICENSE).

---

## 🙌 Contributions

Contributions and suggestions are welcome! Feel free to fork the project, submit issues or open pull requests.
