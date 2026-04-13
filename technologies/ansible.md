# Overview
Infrastructure as code tool that defines resources and infrastructure in config files.
### Control Node
A system on which Ansible is installed.
Capable of running Ansible commands (`ansible` or `ansible-inventory`)
### Inventory
A list of managed nodes that are logically organized. You create an inventory on the control node to describe host deployments to Ansible.
#### Example
ini format
```ini
[myhosts]
192.0.2.50
192.0.2.51
192.0.2.52
```
yaml format
```yaml
myhosts:
  hosts:
    my_host_01:
      ansible_host: 192.0.2.50
      http_port: 80 # example variable for host
    my_host_02:
      ansible_host: 192.0.2.51
    my_host_03:
      ansible_host: 192.0.2.52
  vars:
	  ansible_user: my_server_use # example vars for each host

datacenter: # example metagroup with 1 child group
  children:
    myhosts:
```
- Group hosts according to what for (UI, DB, Backend)
- Group hosts according to where (On-premise, Cloud, Edge)
- Group hosts according to when (Dev, Test, QA, Prod)
#### Commands
Verify Inventory: `ansible-inventory -i inventory.ini --list`
Ping Inventory group: `ansible myhosts -m ping -i inventory.ini`
- Pass `-u` option with ansible if username is different on the control node and the managed node
### Managed Node
A remote system/host that Ansible controles
### Ansible Structure
```
roles/
  common/
    tasks/
    handlers/
    files/              # 'copy' will refer to this
    templates/          # 'template' will refer to this
    meta/               # Role dependencies here
    vars/
    defaults/
      main.yml
```
### Ansible Playbook
Scripts to automate tasks by declaring desired state of the system
```yaml
- name: Playbook name
  hosts: all
  become: true
  # Var files here
  vars_files:
    - revcom-versions.yaml
  # Vars here
  vars:
    host_ip: "hosts.docker.internal"
  # Roles here
  roles:
    - <role 1>
    - <role 2>
    - ...
    - <role n>
```
### Ansible Task
```yaml
- name: DOCKER | Add Docker official GPG key
  ansible.builtin.apt_key:
    url: https://download.docker.com/linux/ubuntu/gpg
    state: present

- name: DOCKER | Set up the stable repository
  ansible.builtin.apt_repository:
    repo: deb [arch=amd64] https://download.docker.com/linux/ubuntu {{ ansible_distribution_release }} stable
    state: present

- name: DOCKER | Install Docker
  ansible.builtin.apt:
    name:
      - apt-transport-https
      - ca-certificates
      - curl
      - gnupg
      - lsb-release
      - docker-ce
      - docker-ce-cli
      - containerd.io
      - docker-buildx-plugin
      - docker-compose-plugin
    state: present
    update_cache: true

```
# Setup
### Local Control Node with Execution Environments
#### 1. Install Dependencies
- Install Docker, python3, python3-pip
- Install ansible-navigator: `pip3 install ansible-navigator`
- Verify env with `ansible-navigator --version` and `ansible-builder --version`
#### 2. Setup execution-environment.yml
```yaml
version: 3

images:
  base_image:
    name: registry.fedoraproject.org/fedora:42

dependencies:
  python_interpreter:
    package_system: python3
  ansible_core:
    package_pip: ansible-core
  ansible_runner:
    package_pip: ansible-runner
  python:
    - six
    - psutil
  system:
  - openssh-clients
  - sshpass
  galaxy:
    collections:
    - name: community.postgresql
    - name: community.docker
    - name: prometheus.prometheus
```
#### 3. Build EE container image
1. `ansible-builder build --tag postgresql_ee --container-runtime docker`
2. Verify: `docker image list` or in `context/Dockerfile`
#### 4. Setup ansible-navigator.yml
```yaml
ansible-navigator:
  ansible-runner:
    artifact-dir: data
  execution-environment:
    container-engine: docker
    enabled: true
    image: postgresql_ee:latest
    pull:
      policy: missing
    container-options:
      - "--user=0"
  logging:
    file: data/ansible-navigator.log
  mode: stdout
  playbook-artifact:
    enable: false
```
#### 5. Run playbooks with navigator
`ansible-navigator run playbook.yml -i inventory.ini`
### Managed Node
- Python installed
- A user that can connect through SSH to the node with an interactive POSIX shell
# Development with Vagrant
### Vagrantfile
```ruby
# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
  config.vm.box = "ubuntu/jammy64"
  config.vm.box_version = "20241002.0.0"

  config.vm.synced_folder "<roles path>", "/vagrant/roles"

  config.vm.provider "virtualbox" do |vb|
    vb.memory = "8192"
    vb.cpus = "4"
  end

  config.vm.provision "ansible_local" do |ansible|
    ansible.playbook = "<playbook path>"
    ansible.galaxy_roles_path = "/vagrant/roles"
  end
end

```
### Commands
Deploy: `vagrant up`
Deploy changes to roles: `vagrant reload --provision`
Teardown: `vagrant destroy`
SSH: `vagrant ssh`
See state of all active Vagrant envs: `vagrant global-status`
Suspend VM: `vagrant suspend`
Resume VM: `vagrant resume`
Stop without destroying: `vagrant halt`
