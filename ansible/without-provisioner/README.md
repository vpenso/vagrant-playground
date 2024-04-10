Basic commands to start and stop the virtual machines…

```bash
# ...start a virtual machine
vagrant up alpha

# ...stop a virtual machine
vagrant destroy alpha

# ...login over SSH
vagrant ssh alpha
```

```bash
# ...set the path to the configuration file
>>> export ANSIBLE_CONFIG=ansible.cfg

# ...list the host inventory
>>> ansible all --list-hosts
  hosts (2):
    alpha
    beta

# ...test access to one host
>>> ansible -m ping alpha   
alpha | SUCCESS => {
    "ansible_facts": {
        "discovered_interpreter_python": "/usr/libexec/platform-python"
    },
    "changed": false,
    "ping": "pong"
}

# ...run  command on both virtual machines
>>> ansible -oa 'hostname' example
beta | CHANGED | rc=0 | (stdout) beta
alpha | CHANGED | rc=0 | (stdout) alpha
```

