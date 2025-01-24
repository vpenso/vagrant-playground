# Talos Linux

Download Talos components from GitHub[^cxhRe]

- **`talosctl`** — Talos CLI client 
- **`metal-amd64.iso`** — Talos ISO
- **`kubectl`**[^Ks3tS] — Kubernetes CLI client

`VagrantFile`[^lVjQq] —  Boot machines from Talos Linux ISO


## Single Controller & Worker

```bash
vagrant up cp1
vagrant up wn1

# print the IP addresses of the machines
virsh list | tail -n+3 | awk '{print $2}' | xargs -t -L1 virsh domifaddr

talosctl gen config test https://$ip_cp1:6443 --install-disk /dev/vda
talosctl -n $ip_cp1 apply-config --insecure --file controlplane.yaml
talosctl -n $ip_wn1 apply-config --insecure --file worker.yaml 
talosctl --nodes $ip_cp1 --endpoints $ip_cp1 bootstrap
talosctl --nodes $ip_cp1 --endpoints $ip_cp1 health
talosctl --nodes $ip_cp1 --endpoints $ip_cp1 kubeconfig ./kubeconfig
kubectl --kubeconfig ./kubeconfig get node -owide
```

## 3 Node Controller Plane 

```bash
vip=192.168.121.100
talosctl gen config test https://$vip:6443 --install-disk /dev/vda
export TALOSCONFIG=$(realpath ./talosconfig)
```

Configure the cluster API endpoint

```yaml
# controlplane.yaml
network:
  interfaces:
    - interface: ens5 # make sure this is correct
      dhcp: true
      vip:
        ip: 192.168.121.100
```


```bash
# validate the modified configuration file
talosctl validate -m metal -c controlplane.yaml

# modifying the machine configuration (installs & reboots) 
talosctl -n $ip_cp1 apply-config --insecure --file controlplane.yaml
talosctl -n $ip_cp2 apply-config --insecure --file controlplane.yaml
talosctl -n $ip_cp3 apply-config --insecure --file controlplane.yaml
talosctl -n $ip_wn1 apply-config --insecure --file worker.yaml
talosctl -n $ip_wn2 apply-config --insecure --file worker.yaml
# wait for some time

talosctl config endpoint $ip_cp1 $ip_cp2 $ip_cp3
talosctl --nodes $ip_cp1 bootstrap
talosctl config node $ip_cp1

talosctl get members
talosctl health

# verify that the interface name is correct
talosctl -n $ip_cp1,$ip_cp2,$ip_cp3 get addresses
# in case the VIP interface name needs to be adjusted
talosctl edit machineconfig

talosctl kubeconfig ./kubeconfig
export KUBECONFIG=$(realpath kubeconfig)
kubectl get node -owide
```

### References

[^cxhRe]: Talos Releases, GitHub  
<https://github.com/siderolabs/talos/releases>

[^lVjQq]: Vagrant & Libvirt, Talos Documentation   
<https://www.talos.dev/v1.9/talos-guides/install/virtualized-platforms/vagrant-libvirt/>

[^Ks3tS]: Kubernetes Releases  
<https://kubernetes.io/releases/download/>
