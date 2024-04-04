Example deployment of Prometheus [^drUjk] &  Grafana [^ueDCq]…

- …using the **Ansible** [^p3z9q] configuration in the
  [`provision/`](provision/) sub-directory
- Services are deployed with containers using the **Podman** container run-time…
  - …they including the `prometheus` server, a `node-exporter` and `grafana`
  - …all containers share a common network namespace using a **Pod** called `monitoring`

### Deployment

Check the service state after `vagrant up`:

```bash
# Check the pod status
>>> podman pod list
POD ID        NAME        STATUS      CREATED         INFRA ID      # OF CONTAINERS
8c47d6e6490e  monitoring  Running     11 minutes ago  4f5de01bf283  4

# …or use the corresponding Systemd service unit
>>> systemctl status pod-monitoring.service
#...

# Containers have individual Systemd service units
>>> systemctl status container-prometheus.service
#...
```

Access the web-interfaces…

- Prometheus <http://192.168.124.11:9090>
- Grafana <http://192.168.124.11:3000> …login as `admin` password `secret123`

## Configuration

The service configuration files in [`provision/files/etc/`](provision/files/etc)
are synchronized during deployment:

- …to the corresponding sub-directories `/etc/{grafana,prometheus}`
- …data storage volumes mounted to `/srv/{grafana,promtheus}`

Use `podman logs $container_name` for debugging the services

[^drUjk]: Prometheus Project  
<https://prometheus.io/docs>  
<https://github.com/prometheus/prometheus>  
<https://quay.io/repository/prometheus/prometheus>

[^ueDCq]: Grafana Project  
<https://grafana.com/oss>  
<https://grafana.com/docs/grafana/latest>  
<https://github.com/grafana/grafana>  
<https://hub.docker.com/r/grafana/grafana>

[^p3z9q]: Ansible Provisioner, Vagrant Documentation  
<https://developer.hashicorp.com/vagrant/docs/provisioning/ansible_intro>  
<https://developer.hashicorp.com/vagrant/docs/provisioning/ansible>  
<https://developer.hashicorp.com/vagrant/docs/provisioning/ansible_common>

