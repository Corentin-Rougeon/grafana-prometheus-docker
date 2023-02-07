# Configuration


### metrics configuration
`prometheus.yml `
```yml
global:
  scrape_interval:     15s # Set the scrape interval to every 15 seconds. Default is every 1 minute.
  evaluation_interval: 15s # Evaluate rules every 15 seconds. The default is every 1 minute.
  # scrape_timeout is set to the global default (10s).

alerting:
  alertmanagers:
    - static_configs:
      - targets: ["alertmanager:9093"]

# Load rules once and periodically evaluate them according to the global 'evaluation_interval'.
rule_files:
  - /etc/prometheus/alert_rules.yml

# A scrape configuration containing exactly one endpoint to scrape:
# Here it's Prometheus itself.
scrape_configs:
  # The job name is added as a label `job=<job_name>` to any timeseries scraped from this config.
  - job_name: 'vad-metrics'
    metrics_path: '/metrics'
    scrape_interval: 5s
    static_configs:
      - targets: ['<YOUR_AGENT_IP_HERE>']
```


### alert configuration
`alertmanager.conf `
```yml
groups:  
  - name: <your_group_name>
    rules:
      - alert: <your_alert_name>
        # Condition for alerting (expression must have a differential expression like < ; > ; =
        expr: <your_prometheus_expression>
        # Annotation - additional informational labels to store more information
        annotations:
          title: '<your_alert_tittle>
          description: '<your_alert_description>'
        # Labels - additional labels to be attached to the alert
        labels:
          severity: '<your_severity>'
```


# Setup


```bash
$ docker compose up
```

# Usage

### grafana dashboard
`127.0.0.1:3000`

### prometheus dashboard
`127.0.0.1:9090`

### alertmanager dashboard
`127.0.0.1:9093`

# docker image requirements

`prometheus`
`grafana/grafana`
`alertmanager`
