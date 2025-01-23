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

### References

[^cxhRe]: Talos Releases, GitHub  
<https://github.com/siderolabs/talos/releases>

[^lVjQq]: Vagrant & Libvirt, Talos Documentation   
<https://www.talos.dev/v1.9/talos-guides/install/virtualized-platforms/vagrant-libvirt/>

[^Ks3tS]: Kubernetes Releases  
<https://kubernetes.io/releases/download/>
