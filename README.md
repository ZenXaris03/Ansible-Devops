# Project set up
* create an inventory file (e.g. hosts or hosts.yaml) that holds the remote hosts that ansible will handle.
* Example entry is
```yaml
webserver: # <-- group
  hosts: # <-- List of hosts in group
    gcloud_host: # <-- host number 1 in group
      ansible_host: <host_ip>
      ansible_port: 22
      ansible_ssh_user: user1
    app01:  # <-- host number 2 in group
      ansible_host: app01
    app02:  # <-- host number 3 in group
      ansible_host: app02
  vars:  # <-- common variables in this group
    ansible_python_interpreter: /usr/bin/python3
```
* to test if all hosts are accesible, run
```bash
ansible -m ping all
```
* to test if a group of hosts are accesible, run
```bash
ansible -m ping all <group-name>
```

* run a playbook
```bash
ansible-playbook -l dbserver-vm playbooks/postgres.yaml

ansible-playbook playbooks/postgres.yaml -l azure-db-server

ansible-playbook playbooks/spring.yaml -l gcloud-app-server

ansible-playbook playbooks/vuejs.yaml -l frontend-vm

ansible-playbook playbooks/main.yaml

ansible-playbook playbooks/spring-vue-docker.yaml -l docker-server
```

Links:
* [Managing host key checking](https://docs.ansible.com/ansible/latest/user_guide/connection_details.html)


## Get host basic info
```bash
ansible-playbook -l <hostname> playbooks/hostvars_and_facts.yml
```

## postgres from ansible-galaxy
install postgresql role
```bash
ansible-galaxy install geerlingguy.postgresql
```


## Links
* [apt module](https://docs.ansible.com/ansible/latest/collections/ansible/builtin/apt_module.html)
* [file module](https://docs.ansible.com/ansible/latest/collections/ansible/builtin/file_module.html)
* [copy module](https://docs.ansible.com/ansible/latest/collections/ansible/builtin/copy_module.html)
* [service module](https://docs.ansible.com/ansible/latest/collections/ansible/builtin/service_module.html)
* [debconf module](https://docs.ansible.com/ansible/latest/collections/ansible/builtin/debconf_module.html)
* [ansible postgres role](https://galaxy.ansible.com/geerlingguy/postgresql)