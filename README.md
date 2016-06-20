# Ansible Role: PCT [![Build Status](https://travis-ci.org/deveth0/ansible-pct.svg?branch=master)](https://travis-ci.org/deveth0/ansible-pct)

Connects to a Proxmox Hypervisor and creates LXC Container using the pct command.
Afterwards it copies over the first SSH Key of the root user to the new container.

## Installation

You can either use ansible-galaxy to install this role:

    ansible-galaxy install deveth0.pct

Or checkout this git-repository to your roles directory:

    git clone https://github.com/deveth0/ansible-pct.git deveth0.pct


## Role Variables

Available variables are listed below, along with the default values:

| Variable | Default | Usage |
| -------- | -------- | -------- | 
| lxc_hypervisor | | The IP of the Proxmox hypervisor to use|
| lxc_id | | The ID of the new container |
| lxc_hostname | | The hostname of the new container |
| lxc_template | | Path of the template to use for the container |
| lxc_memory | 512 | Memory assigned to the new container |
| lxc_swap | 512 | Swap assigned to the new container |
| lxc_cpu_limit | 2 | CPUs assigned to the new container|
| lxc_disk | 8 | Diskspace assigned to the new container|
| lxc_storage | local | Storage used for the new container |
| lxc_net_ip | | IP assigned to the new container |
| lxc_net_netmask |24 | Netmask assigned to the new container |
| lxc_net_gw | | Default Gateway used in the new container |
| lxc_net_bridge |vmbr0 | Network Bridge assigned to the new container
| lxc_nameserver | | Default Nameserver used in the new container |


## Dependencies

No dependencies required

## Example Playbook


    name: Create LXC VM
    hosts: newVMs
    # It's important to disable gather_facts as the new VMs are not available here
    gather_facts: False

    vars:
      lxc_net_gw: 10.0.2.1
      lxc_hostname: foo.bar
      lxc_template: /var/lib/vz/template/cache/debian-8.0-standard_8.4-1_amd64.tar.gz
      lxc_nameserver: 8.8.8.8
      lxc_storage: local-dir
      lxc_hypervisor: 10.0.2.10

    roles:
      - role: deveth0.pct

## Example Hosts

This host file creates two Container

    [newVMs]
    10.0.2.51 lxc_net_ip=10.0.2.51 lxc_id=251
    10.0.2.52 lxc_net_ip=10.0.2.52 lxc_id=252


## License

Apache License 2.0

## Author Information

This Role was created by [Alex Muthmann](http://dev-eth0.de).
