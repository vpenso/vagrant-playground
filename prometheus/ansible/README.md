Example deployment of Prometheus [^drUjk] &  Grafana [^ueDCq]…

- …using the Ansible [^p3z9q] [^RQw4w] configuration in the
  [`provision/`](`provision`) sub-directory
- Access the web-interfaces…
  - Prometheus <http://192.168.124.11:9090>
  - Grafana <http://192.168.124.11:3000> …login as `admin` password `secret123`

Service configuration in [`etc/`](`provision/files/etc`) is synchronized during
deployment.

```bash
# check the pod staus
>>> podman pod list --ctr-names
POD ID        NAME        STATUS      CREATED         INFRA ID      NAMES
8c47d6e6490e  monitoring  Running     10 minutes ago  4f5de01bf283
8c47d6e6490e-infra,grafana,prometheus,node-exporter

>>> podman ps
CONTAINER ID  IMAGE                                    COMMAND
CREATED         STATUS         PORTS
NAMES
4f5de01bf283  localhost/podman-pause:4.6.1-1709719721                        10
minutes ago  Up 10 minutes  0.0.0.0:3000->3000/tcp, 0.0.0.0:9090->9090/tcp
8c47d6e6490e-infra
91238260d159  quay.io/prometheus/node-exporter:v1.7.0                        10
minutes ago  Up 10 minutes  0.0.0.0:3000->3000/tcp, 0.0.0.0:9090->9090/tcp
node-exporter
6dd94006e1d4  quay.io/prometheus/prometheus:v2.45.4    --config.file=/et...  9
minutes ago   Up 9 minutes   0.0.0.0:3000->3000/tcp, 0.0.0.0:9090->9090/tcp
prometheus
5a5ea11007a5  docker.io/grafana/grafana-oss:10.2.6                           8
minutes ago   Up 8 minutes   0.0.0.0:3000->3000/tcp, 0.0.0.0:9090->9090/tcp
grafana
```

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
