
Test-environment for [Incus][4TaLl] from the Linux Containers project

[4TaLl]: https://linuxcontainers.org/incus/docs/main/installing

Make sure to enable nested virtualization on your host:

```bash
echo "options kvm_intel nested=1" \
      | sudo tee /etc/modprobe.d/kvm.conf
```


