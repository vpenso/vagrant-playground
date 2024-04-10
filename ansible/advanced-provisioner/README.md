Example uses the Ansible provisioner [^p3z9q] to configure the Vagrant instance…

```bash
# install Ansible on your host machine
sudo dnf install -y ansible
vagrant up
```

[`provision/`](provision/) holds the Ansible playbook [^D4obz] configuration:

Path | Description
-----|--------------
`main.yml` | Playbook executed by the Vagrant Ansible Provisioner
`vars` | Variables [^65gbG] defined for the playbook
`tasks` | Tasks used by the playbook
`files` | Files used by the plabook
`handlers` | Handlers [^QmiJU] used by the playbook
`templates` | Templates [^uoX3u] used by the playbook

[^p3z9q]: Ansible Provisioner, Vagrant Documentation  
<https://developer.hashicorp.com/vagrant/docs/provisioning/ansible_intro>  
<https://developer.hashicorp.com/vagrant/docs/provisioning/ansible_common>  
<https://developer.hashicorp.com/vagrant/docs/provisioning/ansible>

[^D4obz]: Ansible Playbooks, Ansible Documentation  
<https://docs.ansible.com/ansible/latest/playbook_guide/playbooks_intro.html>

[^65gbG]: Ansible Variables, Ansible Documentation  
<https://docs.ansible.com/ansible/latest/playbook_guide/playbooks_variables.html>

[^QmiJU]: Ansible Handlers, Ansible Documentation  
<https://docs.ansible.com/ansible/latest/playbook_guide/playbooks_handlers.html>

[^uoX3u]: Ansible Template Module, Ansible Documentation  
<https://docs.ansible.com/ansible/latest/collections/ansible/builtin/template_module.html>
