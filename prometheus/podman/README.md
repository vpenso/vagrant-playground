
Open <http://192.168.124.11:9090> to connect with the Prometheus server GUI…

Files | Description
------|--------------
[`prometheus-pod.yml`][01] | YAML Definition for a Prometheus server as Podman pod
[`prometheus.yml`][02] | Prometheus server configuration file

[01]: prometheus-pod.yml
[02]: prometheus.yml

```sh
# after modifications to the configuration …restart the server
podman restart prometheus-prometheus-server
# check the logs
podman logs prometheus-prometheus-server
```

