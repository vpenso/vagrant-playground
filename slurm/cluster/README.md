

```bash
# load the configuration file and enable the custom network
virsh net-define custom.xml && virsh net-start custom

# start the control plane
vagrant up wlm1
```
