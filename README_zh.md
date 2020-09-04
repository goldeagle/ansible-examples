# ThinkPHP.Tech/Ansible-Examples | [English](README.md)
Thinkphp 的 ansible 剧本（playbook），依赖 ansible galaxy 上的 [thinkphp_tech.thinkphp](https://galaxy.ansible.com/thinkphp_tech/thinkphp) 集合。

[Ansible](https://www.ansible.com) 是基于 python 语言开发的自动化运维工具，类似的还有 saltstack 等。Ansible 剧本（playbook）是指通过 ansible 工具运行的批量任务，ansible 集合（collection）和角色（role）是指通过一定规则组织好的批量任务。

## 使用方法

### 安装 ansible
首先，下载安装 ansible 工具
- Linux:
```bash
$ apt install ansible
```

- MacOS:
```bash
$ brew install ansible
```

- Github 仓库
```bash
$ git clone https://github.com/ansible/ansible
```

### 安装 thinkphp_tech.thinkphp 集合

安装集合：
```bash
$ ansible-galaxy collection install thinkphp_tech.thinkphp
```

默认情况下，集合会被安装到：
```bash
~/.ansible/collections/ansible_collections/thinkphp_tech/thinkphp/
```
### 编写执行的剧本
接下来就可以自定一个剧本文件使用集合里面包含的角色，（比如叫 playbook.yml）：

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

也可以参考一下仓库里面的例子： [playbook_example.yml](playbook_example.yml)

### 编辑主机文件

要确认需要自动管理的主机信息都已经放到清单文件。

默认的清单文件一般在 /etc/ansible/hosts，

或者也可以自己定义一个清单文件，然后用 '-i' 参数调用。

这里有个主机清单文件的例子： [hosts_example](hosts_example)

### 运行

运行剧本文件：

```bash
$ ansible-playbook -i <your_hosts_file> playbook.yml -K
```

### 更多参考

thinkphp_tech.thinkphp [官方仓库](https://github.com/thinkphp_tech/ansible-collection-thinkphp)

关于 Ansible 的更多使用方法请参考[官方手册](https://docs.ansible.com/ansible/latest/user_guide/)