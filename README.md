# ThinkPHP.Tech/Ansible-Examples | [中文](README_zh.md)
Ansible playbooks for thinkphp, depends on ansible galaxy [thinkphp_tech.thinkphp](https://galaxy.ansible.com/thinkphp_tech/thinkphp) collection.

[Ansible](https://www.ansible.com) is an automantic operation tool by python, such as saltstack etc.. Ansible playbook is a task list for ansible. Ansible collections and roles are tasks arranged by rules.

## Usage

### Install ansible
First of all, download "ansbile"
- Linux:
```bash
$ apt install ansbile
```

- MacOS:
```bash
$ brew install ansbile
```

- Github 仓库
```bash
$ git clone https://github.com/ansible/ansible
```

### Install collection

Install this collection:
```bash
$ ansible-galaxy collection install thinkphp_tech.thinkphp
```

By default, the collection will be installed here:  
```bash
~/.ansible/collections/ansible_collections/thinkphp_tech/thinkphp/
```
### Edit playbook
Then you can use the roles from the collection in your playbooks (playbook.yml etc.):

```yaml
---

- name : configure and deploy the local servers and app codes
  hosts: {{ your_host_group_in_your_inventory }}
  remote_user: {{ your_remote_ansible_user }}
  become: yes
  become_method: sudo

  vars:
    ansible_python_interpreter: /usr/bin/python3
    php_install_composer: true
    php_install_pecl: true
    php_install_swoole: true

  collections:
    - thinkphp_tech.thinkphp

  roles:
    - common
    - nginx
    - php
    - redis
    - git
```

Also you can take a look at [playbook_example.yml](playbook_example.yml) in this repository.

### Edit hosts

Make sure you have your hosts infomation in the inventory file.

The default inventory file path is: /etc/ansible/hosts

Or you can specify your personal one with the '-i' parameter.

Here is an example file: [hosts_example](hosts_example)

### Run

Run the playbook:

```bash
$ ansible-playbook -i <your_hosts_file> playbook.yml -K
```

### References

thinkphp_tech.thinkphp [collection repository](https://github.com/thinkphp_tech/ansible-collection-thinkphp)

More refernces abort ansible: [Official Docs](https://docs.ansible.com/ansible/latest/user_guide/)