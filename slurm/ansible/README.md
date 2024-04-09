Example uses the Ansible provisioner [^p3z9q] to configure the Vagrant instance…

```bash
# install Ansible on your host machine
sudo dnf install -y ansible
vagrant up
```

Sub-directory [`provision/`](provision/) holds the Ansible [^D4obz]
configuration.

[^p3z9q]: Ansible Provisioner, Vagrant Documentation  
<https://developer.hashicorp.com/vagrant/docs/provisioning/ansible_intro>  
<https://developer.hashicorp.com/vagrant/docs/provisioning/ansible_common>  
<https://developer.hashicorp.com/vagrant/docs/provisioning/ansible>

[^D4obz]: Ansible Roles, Ansible Documentation  
<https://docs.ansible.com/ansible/latest/playbook_guide/playbooks_reuse_roles.html>

