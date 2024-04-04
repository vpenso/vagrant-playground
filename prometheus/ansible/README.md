Example deployment of Prometheus [^drUjk] &  Grafana [^ueDCq]…

- …using the Ansible [^p3z9q] [^RQw4w] configuration in the
  [`provision/`](provision/) sub-directory
- Access the web-interfaces…
  - Prometheus <http://192.168.124.11:9090>
  - Grafana <http://192.168.124.11:3000> …login as `admin` password `secret123`

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

Service configuration in [`provision/files/etc/`](provision/files/etc) is 
synchronized during deployment 

- …to sub-directories `/etc/{prometheus,grafana}`
- …data storage volumes mounted to `/srv/promehteus` and `/var/lib/grafana`

[^drUjk]: Prometheus Project  
<https://github.com/prometheus/prometheus>  
<https://prometheus.io/docs>

[^ueDCq]: Grafana Project  
<https://grafana.com/oss>  
<https://grafana.com/docs/grafana/latest>  
<https://github.com/grafana/grafana>

[^p3z9q]: Ansible Provisioner, Vagrant Documentation  
<https://developer.hashicorp.com/vagrant/docs/provisioning/ansible_intro>  
<https://developer.hashicorp.com/vagrant/docs/provisioning/ansible>

[^RQw4w]: Ansible Options, Vagrant Documentation  
<https://developer.hashicorp.com/vagrant/docs/provisioning/ansible_common>
