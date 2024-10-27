# Monitoring
Basic monitoring setup via Docker Compose using Prometheus and Grafana.

## Grafana Dashboards
- [Node Exporter Full](https://grafana.com/grafana/dashboards/1860-node-exporter-full/)
- [Prometheus Blackbox Exporter](https://grafana.com/grafana/dashboards/7587-prometheus-blackbox-exporter/)
- [cAdvisor Exporter](https://grafana.com/grafana/dashboards/14282-cadvisor-exporter/)
- [Traefik Official Standalone Dasbhoard](https://grafana.com/grafana/dashboards/17346-traefik-official-standalone-dashboard/)

## Setup Alertmanager File
```bash
export $(cat .env | xargs)
envsubst < alertmanager/alertmanager.yml.tmpl > alertmanager/alertmanager.yml
envsubst < prometheus/prometheus.central.yml.tmpl > prometheus/prometheus.central.yml
envsubst < prometheus/prometheus.node.yml.tmpl > prometheus/prometheus.node.yml
```

## Rules
The used rules are mostly from/inspired by [awesome-prometheus-alerts](https://samber.github.io/awesome-prometheus-alerts/rules).
