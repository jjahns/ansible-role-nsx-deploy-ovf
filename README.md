# Ansible Role: nsx-deploy-ovf

## Description

Deploy a NSX-T virtual appliance (OVF/OVA) to a vSphere environment.

## Requirements

* pyVmomi (install via pip)
* pyVim (install via pip)
* ansible (latest release)
* NSX-T OVF/OVA Appliances, 2.2 or later

## Installation

Install using Ansible Galaxy:

```
$ ansible-galaxy install jjahns.nsx_deploy_ovf
```

## Role Variables

Ansible variables are listed below, with default values located in `defaults/main.yml`.

```
nsx_ovf_vsphere_hostname:
nsx_ovf_vsphere_username: administrator@vsphere.local
nsx_ovf_vsphere_password:
nsx_ovf_vsphere_validate_certs: yes
nsx_ovf_datacenter:
nsx_ovf_cluster:
nsx_ovf_datastore:
nsx_ovf_networks:
nsx_ovf_path:
nsx_ovf_allow_duplicates: no
nsx_ovf_deployment_option: medium
nsx_ovf_disk_provisioning: thin
nsx_ovf_fail_on_spec_warnings: yes
nsx_ovf_vmname: "{{ inventory_hostname }}"
nsx_ovf_power_on: yes
nsx_ovf_enable_ssh: no
nsx_ovf_enable_root_ssh: no
nsx_ovf_vmhostname: "{{ inventory_hostname }}"
nsx_ovf_wait: yes
nsx_ovf_wait_for_ip_address: yes
nsx_ovf_ip_address:
nsx_ovf_netmask:
nsx_ovf_gateway:
nsx_ovf_dns_servers:
nsx_ovf_domain:
nsx_ovf_ntp_servers:
nsx_ovf_password:
nsx_ovf_root_password:
nsx_ovf_folder:
nsx_ovf_resource_pool:
```

## Example Playbooks

```yaml
- hosts: nsx-manager[0]
  gather_facts: no
  connection: local
  vars:
    nsx_ovf_vsphere_hostname: my-vcenter.local.localdomain
    nsx_ovf_vsphere_password: my_administrator_password
    nsx_ovf_datacenter: mydc
    nsx_ovf_cluster: mycluster
    nsx_ovf_datastore: mydatastore
    nsx_ovf_networks: 
      OVF Network Name: vmware-portgroup-name
    nsx_ovf_path: /path/to/nsx/appliance.ova
    nsx_ovf_role: nsx-manager
    nsx_ovf_ip_address: 192.168.1.10
    nsx_ovf_netmask: 255.255.255.0
    nsx_ovf_gateway: 192.168.1.1
    nsx_ovf_dns_servers:
      - 192.168.1.2
      - 192.168.1.3
    nsx_ovf_domain: local.localdomain
    nsx_ovf_ntp_servers:
      - 192.168.1.2
      - 192.168.1.3
    nsx_ovf_password: my_admin_password_to_nsx
    nsx_ovf_root_password: my_root_password_to_nsx
  roles:
    - jjahns.nsx-deploy-ovf
```
## License

This project is licened under [BSD-2](https://opensource.org/licenses/BSD-2-Clause) License. See [LICENSE](/LICENSE) for more details.

## Dependencies

None.

