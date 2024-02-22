Make sure to enable nested virtualization on your host:

```bash
echo "options kvm_intel nested=1" \
      | sudo tee /etc/modprobe.d/kvm.conf
```


