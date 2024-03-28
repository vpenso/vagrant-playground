
Open <http://192.168.124.11:9090> to connect with the Prometheus server GUI…

Files | Description
------|--------------
[`prometheus-pod.yml`][01] | YAML Definition for a Prometheus server as Podman pod
[`prometheus.yml`][02] | Prometheus server configuration file

[01]: prometheus-pod.yml
[02]: prometheus.yml

### Configuration

Example of extending the scraper configuration…

```sh
cat > /etc/prometheus/scrape_config.d/promlab.yml <<EOF
scrape_configs:
- job_name: 'promlab'
  static_configs:
  - targets:
    - demo.promlabs.com:10000
    - demo.promlabs.com:10001
    - demo.promlabs.com:10002
EOF

# after modifications to the configuration …restart the server
podman restart prometheus-prometheus-server

# check the logs for errers in the configuration
podman logs prometheus-prometheus-server
```

