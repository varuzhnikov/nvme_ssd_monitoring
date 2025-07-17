# SSD Health Monitoring on Bare-Metal Servers

> End-to-end setup for monitoring NVMe SSD health using smartctl, Prometheus, and Grafana. Ideal for dedicated servers (Hetzner, OVH, etc).

---

## 📈 What This Project Does

This repository helps you:
- ✅ Check NVMe SSD health manually using `smartctl`
- ✅ Collect SMART metrics with Prometheus via `smartctl_exporter`
- ✅ Trigger alerts for early SSD failure detection
- ✅ Visualize health metrics in Grafana
- ✅ Replace disks before they die unexpectedly

---

## 🛠 Stack Used

- `smartctl` from `smartmontools`
- `smartctl_exporter` (Go-based Prometheus exporter)
- Prometheus
- Grafana

---

## 📦 What's Included

| Folder       | Contents                                                |
|--------------|---------------------------------------------------------|
| `grafana/`   | Grafana dashboard JSON with all SSD panels              |
| `prometheus/`| Prometheus alert rules (`smartctl_alerts.yml`)         |
| `systemd/`   | Ready-to-use `smartctl_exporter` systemd unit file      |
| `exporter/`  | Build instructions for `smartctl_exporter` from source |

---

## 🚀 Quickstart

1. **Install smartmontools**
   ```bash
   sudo apt install smartmontools
   ```

2. **Clone and build smartctl_exporter**
   ```
   git clone https://github.com/prometheus-community/smartctl_exporter
   cd smartctl_exporter
   go build
   ```
3. **Install the exporter binary**

   ```
   sudo cp smartctl_exporter /usr/local/bin/
   ```

4. **Use the systemd unit from systemd/**
   Enable it with:
   ```
   sudo systemctl daemon-reload
   sudo systemctl enable smartctl_exporter
   sudo systemctl start smartctl_exporter
   ```
5. Configure Prometheus
   * Add job config from prometheus/
   * Add alert rules from smartctl_alerts.yml to rule_files

6. Import Grafana dashboard
   * Use the file grafana/ssd_dashboard.json
