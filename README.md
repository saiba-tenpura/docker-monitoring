# Monitoring
Basic monitoring setup via Docker Compose using Prometheus and Grafana.

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

## Rules
The used rules are mostly from/inspired by [awesome-prometheus-alerts](https://samber.github.io/awesome-prometheus-alerts/rules).

## License
[MIT](./LICENSE)
