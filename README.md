# 🚀 Server Monitoring Automation Setup

Easily automate your server monitoring setup with this Docker Compose configuration. This setup includes **cAdvisor**, **Prometheus**, **Loki**, and **Grafana**, providing you with powerful tools to monitor your servers' performance, logs, and resource utilization.

---

## 📋 Features
- **cAdvisor**: Collects metrics about resource usage and performance of running containers.
- **Prometheus**: Time-series database for collecting and querying metrics.
- **Loki**: Lightweight, cost-effective log aggregation system.
- **Grafana**: Visualizes metrics and logs with beautiful dashboards.

---

## 🛠 Prerequisites
1. Ensure **Docker** and **Docker Compose** are installed on your system.
   - [Install Docker](https://docs.docker.com/get-docker/)
   - [Install Docker Compose](https://docs.docker.com/compose/install/)
2. Make sure the external network `monitoring-internal-network` exists. If not, create it:
   ```bash
   docker network create monitoring-internal-network
   ```
3. Install Docker’s Loki logging plugin:
   ```bash
   docker plugin install grafana/loki-docker-driver:latest --alias loki --grant-all-permissions
   ```

---

## 📂 File Structure
- Your project structure should look like this:
```bash
monitoring-server
├── compose.yaml
├── loki
│   └── loki-config.yml
└── prometheus
    └── prometheus.yml
```

---

## 🚀 Quick Start

Follow these steps to spin up the monitoring stack:

##### 1️⃣ Clone the Repository
Use the following address to get the repo.

```bash
git clone https://github.com/abhaywani114/server-monitoring-setup.git
cd server-monitoring-setup
```

##### 2️⃣ Spin Up the Stack
Run the following command to start all services:

```bash
docker-compose -f compose.yaml up -d
```

##### 3️⃣ Access the Services

- cAdvisor: http://localhost:8080
- Prometheus: http://localhost:9090
- Loki: http://localhost:3100
- Grafana: http://localhost:3000
    * Default Username: `admin`
    * Default Password: `admin`

---

## 🔧 Configure Log Forwarding to Loki
To send container logs to Loki, configure the logging driver in your service definitions. Here's an example snippet:
```yml
services:
  my-service:
    image: my-image:latest
    logging:
      driver: loki
      options:
        loki-url: http://localhost:3100/loki/api/v1/push
        loki-batch-size: "400"
```
Restart the container for the changes to take effect.

##  📊 Configure Grafana Dashboards
1. Log in to Grafana at http://localhost:3000.
2. Add Prometheus and Loki as data sources:
3. Prometheus URL: http://prometheus:9090
4. Loki URL: http://loki:3100
5. Import prebuilt dashboards for visualizing metrics and logs:
   - **[cAdvisor Dashboard](https://grafana.com/grafana/dashboards/893-main/)**
   - **[Loki Dashboard](https://grafana.com/grafana/dashboards/13186-loki-dashboard/)**

---
## 🤝 Contributing
Feel free to open issues or submit pull requests to improve this project. Contributions are welcome!

---
## 🌟 Support
If you found this helpful, give it a ⭐ on GitHub!

