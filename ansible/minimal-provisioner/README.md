Minimal example how to  use Ansible provisioner [^p3z9q] for a Vagrant instance…

```bash
# install Ansible on your host machine
sudo dnf install -y ansible
```

File | Description
-----|---------------
[`main.yml`](main.yml) | Ansible playbook example

Ansible configuration [^RQw4w] in the [`Vagrantfile`](Vagrantfile):

```ruby
#...
  config.vm.provision "ansible" do |ansible|
    ansible.raw_ssh_args = ['-o UserKnownHostsFile=/dev/null']
    ansible.host_key_checking = false
    #ansible.verbose = 'vvv'
    ansible.playbook = "main.yml"
    ansible.groups = { "http_server" => "test_http_server" }
    ansible.host_vars = { "http_test" => { "http_port" => 8080 } }
  end
#...
```

[^p3z9q]: Ansible Provisioner, Vagrant Documentation  
<https://developer.hashicorp.com/vagrant/docs/provisioning/ansible_intro>  
<https://developer.hashicorp.com/vagrant/docs/provisioning/ansible>

[^RQw4w]: Ansible Options, Vagrant Documentation  
<https://developer.hashicorp.com/vagrant/docs/provisioning/ansible_common>
