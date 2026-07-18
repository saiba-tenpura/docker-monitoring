# Monitoring
Basic monitoring setup via Docker Compose using mainly Prometheus, Grafana as well as a Telegram Bot for sending notifications.

## Grafana Dashboards
- [Node Exporter Full](https://grafana.com/grafana/dashboards/1860-node-exporter-full/)
- [Prometheus Blackbox Exporter](https://grafana.com/grafana/dashboards/7587-prometheus-blackbox-exporter/)
- [cAdvisor Exporter](https://grafana.com/grafana/dashboards/14282-cadvisor-exporter/)
- [Traefik Official Standalone Dasbhoard](https://grafana.com/grafana/dashboards/17346-traefik-official-standalone-dashboard/)

## Traefik Reverse Proxy
For as how to setup the Traefik refer to this [repository](https://github.com/saiba-tenpura/traefik-proxy).

## Central
The central system the Prometheus metrics are federated to which also incl. a Grafana instance to visualize the data, Blackbox exporter for probing systems and Alertmanager for sending notifications as well as everything a regular node runs. 
```
docker compose -f compose.yaml -f compose.central.yaml up -d
```

### Services
- Prometheus
- Node exporter
- cAdvisor
- Grafana
- Alertmanager
- Blackbox exporter

### Setup Configuration
```bash
cp .env.example .env
# Adjust the .env file according to your setup.
export $(cat .env | xargs)
envsubst < alertmanager/alertmanager.yml.tmpl > alertmanager/alertmanager.yml
envsubst < prometheus/prometheus.central.yml.tmpl > prometheus/prometheus.central.yml
```

## Node
A node which scrapes metrics from Prometheus, Node exporter and cAdvisor.
```
docker compose -f compose.yaml -f compose.node.yaml up -d
```

### Services
- Prometheus
- Node exporter
- cAdvisor

### Setup Configuration
```bash
cp .env.example .en
# Adjust the .env file according to your setup.
export $(cat .env | xargs)
envsubst < prometheus/prometheus.node.yml.tmpl > prometheus/prometheus.node.yml
```

## Environment Variables
| Variable | Description |
| -------- | ----------- |
| `NODE_NAME` | Unique identifier for the node/server. Used to label metrics, alerts, or dashboards. |
| `PROMETHEUS_DOMAIN` | Base DOMAIN of the Prometheus server used for querying metrics. |
| `GRAFANA_DOMAIN` | Base DOMAIN of the Grafana instance for dashboards and API access. |
| `ALERTMANAGER_DOMAIN` | Base DOMAIN the Alertmanager service handling alerts. |
| `BLACKBOX_DOMAIN` | Base DOMAIN of the Blackbox Exporter used for endpoint probing. |
| `GRAFANA_ADMIN_USER` | Username for Grafana administrative interface access. |
| `GRAFANA_ADMIN_PASSWORD` | Password for the Grafana admin user. |
| `TELEGRAM_BOT_TOKEN` | API token for a Telegram bot used to send notifications or alerts. |
| `TELEGRAM_CHAT_ID` | Target Telegram chat ID where notifications will be sent. |
| `PROMETHEUS_BASIC_AUTH` | Username for Prometheus basic authentication. |
| `PROMETHEUS_PASSWORD` | Password for Prometheus basic authentication. |

## Rules
The used rules are mostly from/inspired by [awesome-prometheus-alerts](https://samber.github.io/awesome-prometheus-alerts/rules).

## License
[MIT](./LICENSE)
