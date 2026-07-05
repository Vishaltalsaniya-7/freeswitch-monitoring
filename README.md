# VoIP Monitoring Stack Setup Guide

## 1. Download or Clone Project

```bash
git clone https://github.com/Vishaltalsaniya-7/freeswitch-monitoring.git
cd freeswitch-monitoring
```

OR download ZIP:

```
Code → Download ZIP → Extract
```

---

## 2. Configure Environment

```bash
cp .env.example .env
```

Update values:

* FreeSWITCH ESL credentials
* MySQL / PostgreSQL details
* Grafana admin password

---

## 3. Start Stack

```bash
docker compose up -d
```

---

## 4. Access Services

* Grafana → http://localhost:9030
* Prometheus → http://localhost:9090
* Loki → http://localhost:3100
* HOMER → http://localhost:9080

---

## 5. Stop Stack

```bash
docker compose down
```

---

## 6. Reset Stack

```bash
docker compose down -v
```
