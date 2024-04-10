[`Vagrantfile`](Vagrantfile):

- Defines two virtual machine instance `alpha` and `beta`
- Set IP-addresses to 192.168.18.80 and 192.168.18.81

Basic commands to start and stop the virtual machines…

```bash
# ...start a virtual machine
vagrant up alpha

# ...stop a virtual machine
vagrant destroy alpha

# ...login over SSH
vagrant ssh alpha
```

The [`hosts`](hosts) inventory file referencing both virtual machines by IP-address

Ansible configuration file [`ansible.cfg`](ansible.cfg) [^i2FzG]:

[^i2FzG]: Ansible Configuration Settings, Ansible Documentation  
<https://docs.ansible.com/ansible/latest/reference_appendices/config.html>

- Default password as plain-text string (…within configuration is not supported)
- `[default]` section sets user `vagrant` and references the path to the
  file storing the SSH password

Using the configuration with the `ansible` command...

- …set the environment variable `ANSIBLE_CONFIG`
- …check that the host inventory file is correctly parsed
- …use the ping module `-m ping` to establish a connection
- …run a command on all virtual machines instance

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


