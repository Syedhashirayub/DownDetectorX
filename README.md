# 🚀 DownDetectorX

# Real-Time DevOps Monitoring Project

A full-fledged monitoring setup using Prometheus, Alertmanager, Blackbox Exporter, Node Exporter, and custom alerting to monitor infrastructure, apps, and services.

## 🔧 Tools Used
- Prometheus 📊
- Alertmanager 📬
- Node Exporter 🧠
- Blackbox Exporter 🌐
- Java/Maven Sample App (BoardGame 🎮)
- Ubuntu (on AWS EC2)

---

## ⚙️ Architecture Overview

- Node Exporter on VM1 monitors system metrics (CPU, RAM, Disk)
- Blackbox Exporter on Monitoring VM pings websites/services
- Prometheus scrapes all metrics
- Alertmanager triggers email alerts for:
  - Website down
  - Instance down
  - High CPU / RAM
  - Disk full
  - Service stopped

![Screenshot 2025-06-29 at 10 06 30 AM](https://github.com/user-attachments/assets/4b4c1546-c47e-4688-954b-89838dcaa846)

---

## 📩 Alerting Scenarios

| Condition              | Triggered by         | Delay   |
|------------------------|----------------------|---------|
| Website Down           | Blackbox Exporter    | 1 min   |
| Instance Down          | Node Exporter        | 1 min   |
| High CPU Load          | Node Exporter        | 10 min  |
| Out of Memory          | Node Exporter        | 1 min   |
| Service Unavailable    | Node Exporter config | 2 min   |

---

## 🔌 Setup Instructions

### 1. 🖥️ Launch 2 VMs (Ubuntu 24.04)
- VM1: Web app + Node Exporter
- VM2: Prometheus, Alertmanager, Blackbox Exporter

### 2. 🔍 Install Prometheus, Alertmanager, Exporters
See [`setup-scripts/install.sh`](./setup-scripts/install.sh) *(Write install steps in bash)*

### 3. 🧾 Configure Files

- [`prometheus/prometheus.yml`](./prometheus/prometheus.yml)  
  Set scrape jobs for node_exporter & blackbox

- [`prometheus/alert_rules.yml`](./prometheus/alert_rules.yml)  
  Define alerting conditions

- [`alertmanager/alertmanager.yml`](./alertmanager/alertmanager.yml)  
  Configure Gmail app password for SMTP alerts

---

## 🧪 Testing Alerts
1. Kill the app (`CTRL+C`) ➜ Get **Website Down** mail
2. Kill node_exporter ➜ Get **Service Unavailable**
3. Kill VM ➜ Get **Instance Down**

---

## 📬 Email Alerts Demo

✅ Website Down  
✅ Instance Down  
✅ Service Unavailable  

(Screenshots optional)

---

## 💡 Credits
Based on a tutorial by [NoteGPT YouTube Channel](https://www.youtube.com/@NoteGPT)

---

## 📎 License
MIT
