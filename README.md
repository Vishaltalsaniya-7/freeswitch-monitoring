# VoIP Monitoring Stack (FreeSWITCH + OpenSIPS + Observability)

A complete **Docker-based VoIP monitoring and observability platform** for FreeSWITCH and SIP infrastructure using **Prometheus, Grafana, Loki, HOMER, Heplify Server, Node Exporter, and FreeSWITCH Exporters**.

This project provides real-time monitoring for:

- Call metrics
- SIP traffic
- FreeSWITCH health (UP/DOWN)
- CPU / Memory / Disk usage
- MySQL performance
- RTP / SIP debugging

---

## 🚀 Features

- 📞 FreeSWITCH call monitoring (active calls, channels, status)
- 📡 SIP packet capture using HOMER + Heplify
- 🖥 System monitoring (CPU, RAM, Disk, Network)
- 🗄 MySQL performance monitoring
- 📊 Grafana dashboards for visualization
- ⚡ Prometheus metrics collection
- 🧠 Loki centralized logging
- 🐳 Fully Dockerized deployment
- 🔁 Multi FreeSWITCH exporter support

---

## 📦 Architecture

```
                        ┌──────────────────────┐
                        │      Grafana          │
                        │  (Dashboards / UI)    │
                        └───────────┬───────────┘
                                    │
                        ┌───────────▼───────────┐
                        │      Prometheus        │
                        │  (Metrics Aggregation) │
                        └───────────┬───────────┘
           ┌────────────┬───────────┼───────────┬────────────┐
           │             │           │            │            │
   ┌───────▼─────┐ ┌─────▼─────┐ ┌───▼────┐ ┌─────▼──────┐ ┌───▼─────┐
   │Node Exporter│ │FreeSWITCH │ │ MySQL  │ │  Heplify   │ │  Loki   │
   │  (System)   │ │ Exporters │ │Exporter│ │  Server    │ │ (Logs)  │
   └─────────────┘ └───────────┘ └────────┘ └─────┬──────┘ └─────────┘
                                                     │
                                              ┌──────▼──────┐
                                              │  HOMER Web  │
                                              │ (SIP/HEP)   │
                                              └─────────────┘

                        ┌──────────────────────┐
                        │    Alertmanager       │
                        │  (Alerts & Notify)    │
                        └──────────────────────┘
```

---

## ⚙️ Installation

### 1. Clone Repository

```bash
git clone https://github.com/Vishaltalsaniya-7/freeswitch-monitoring.git
cd freeswitch-monitoring
```

### 2. Configure Environment

```bash
cp .env.example .env
```

Update values for:

- FreeSWITCH ESL credentials
- MySQL credentials
- Grafana admin password
- HOMER database settings

### 3. Start Stack

```bash
docker compose up -d
```

---

## 🌐 Service URLs

| Service      | URL                                            |
| ------------ | ----------------------------------------------- |
| Grafana      | [http://localhost:9030](http://localhost:9030) |
| Prometheus   | [http://localhost:9090](http://localhost:9090) |
| Loki         | [http://localhost:3100](http://localhost:3100) |
| HOMER Web    | [http://localhost:9080](http://localhost:9080) |
| Alertmanager | [http://localhost:9093](http://localhost:9093) |

---

## 📊 Prometheus Scrape Config

This stack monitors multiple VoIP and system components:

```yaml
scrape_configs:
  - job_name: 'nodeexporter'
    scrape_interval: 5s
    static_configs:
      - targets: ['nodeexporter:9100']

  - job_name: 'prometheus'
    scrape_interval: 10s
    static_configs:
      - targets: ['localhost:9090']

  - job_name: 'heplify-server'
    scrape_interval: 5s
    static_configs:
      - targets: ['heplify-server:9096']

  # FreeSWITCH Exporter - Agent
  - job_name: 'freeswitch-exporter-local-agent'
    scrape_interval: 15s
    static_configs:
      - targets: ['freeswitch-exporter-local-agent:9282']

  # FreeSWITCH Exporter - Requester
  - job_name: 'freeswitch-exporter-local-requester'
    scrape_interval: 15s
    static_configs:
      - targets: ['freeswitch-exporter-local-requester:9283']

  # MySQL Exporter
  - job_name: 'mysql'
    scrape_interval: 15s
    static_configs:
      - targets: ['mysql-exporter:9104']
```

---

## 📡 Monitoring Capabilities

### 🖥 System Metrics

- CPU usage
- Memory usage
- Disk usage
- Network performance
- System uptime

### ☎️ FreeSWITCH Monitoring

- Active calls
- Call rate (CPS)
- Channel status
- SIP registration status
- FreeSWITCH UP/DOWN status
- ESL health

### 🗄 MySQL Monitoring

- Query performance
- Connections
- Slow queries
- DB uptime

### 📞 SIP & Call Analysis

- SIP INVITE / BYE / REGISTER tracing
- Call flow analysis
- RTP quality issues
- NAT traversal debugging

---

## 📊 Grafana Dashboards

Pre-configured dashboards:

- FreeSWITCH Call Overview
- SIP Call Flow Metrics
- System CPU / Memory
- RTP QoS Monitoring
- MySQL Performance Dashboard
- SIP Error Rates

---

## 🐳 Services Included

- Prometheus
- Grafana
- Loki
- Alertmanager
- Node Exporter
- FreeSWITCH Exporter (2 instances)
- MySQL Exporter
- HOMER SIP Capture
- Heplify Server

---

## 🔥 Use Cases

- VoIP production monitoring
- Call center infrastructure monitoring
- SIP troubleshooting
- FreeSWITCH high availability monitoring
- Real-time call analytics
- DevOps observability for telecom systems

---

## 🛑 Stop Stack

```bash
docker compose down
```

## 🧹 Reset Stack

```bash
docker compose down -v
```

---

## 👨‍💻 Author

**Vishal Talsaniya**
VoIP Engineer | Backend Developer (Golang)
