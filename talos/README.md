# Talos Linux

Download Talos components from GitHub[^cxhRe]

- **`talosctl`** — Talos CLI client 
- **`metal-amd64.iso`** — Talos ISO

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
```

### References

[^cxhRe]: Talos Releases, GitHub  
<https://github.com/siderolabs/talos/releases>

[^lVjQq]: Vagrant & Libvirt, Talos Documentation   
<https://www.talos.dev/v1.9/talos-guides/install/virtualized-platforms/vagrant-libvirt/>
