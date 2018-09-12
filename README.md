# Ansible Role: nsx-ovf

## Description

Deploy a NSX-T virtual appliance (OVF/OVA) to a vSphere environment.

## Requirements

* pyVmomi (install via pip)
* pyVim (install via pip)
* ansible (latest release)
* NSX-T (2.2 or higher)

## Role Variables

All variables with default values are located in [defaults/main.yml](defaults/main.yml) and can be overridden. It is recommended that variables be placed at the host_vars level per NSX-T virtual appliance deployed.

| Name           | Default Value | Description                        |
| -------------- | ------------- | -----------------------------------|
| `nsx_ovf_vsphere_hostname` | | IP/FQDN of vSphere host (vCenter/ESXI) |
| `nsx_ovf_vsphere_username` | administrator@vsphere.local | vSphere user account to deploy virtual appliance with |
| `nsx_ovf_vsphere_password` | | Password of vSphere user account |
| `nsx_ovf_vsphere_validate_certs` | yes | Whether or not to validate vSphere SSL certificates |
 

## Default Variables

Values that are set by default, with the corresponding value.
If you wish to change these values, please define them in your playbook or your host_vars. Do not edit these defaults.

* `nsx_ovf_vsphere_username:` administrator@vsphere.local
* `nsx_ovf_vsphere_validate_certs:` yes
* `nsx_ovf_allow_duplicates:` no
* `nsx_ovf_deployment_option:` medium
* `nsx_ovf_disk_provisioning:` thin
* `nsx_ovf_fail_on_spec_warnings:` yes
* `nsx_ovf_vmname:` "{{ inventory_hostname }}"
* `nsx_ovf_power_on:` yes
* `nsx_ovf_enable_ssh:` no
* `nsx_ovf_enable_root_ssh:` no
* `nsx_ovf_vmhostname:` "{{ inventory_hostname }}"
* `nsx_ovf_wait:` yes
* `nsx_ovf_wait_for_ip_address:` yes

## Required Variables

Values that are not set and are required.
Playbooks will fail to run if calling this role without these variables set either at run time or at the host level. It is not recommended to set properties such as nsx_ovf_ip_address at the group level.

* `nsx_ovf_vsphere_hostname:`
* `nsx_ovf_vsphere_password:`
* `nsx_ovf_datacenter:`
* `nsx_ovf_cluster:`
* `nsx_ovf_datastore:`
* `nsx_ovf_networks:`
* `nsx_ovf_path:`
* `nsx_ovf_ip_address:`
* `nsx_ovf_netmask:`
* `nsx_ovf_gateway:`
* `nsx_ovf_dns_servers:`
* `nsx_ovf_domain:`
* `nsx_ovf_ntp_servers:`
* `nsx_ovf_password:`
* `nsx_ovf_root_password:`

## Optional Variables

Values that are optional but not critical to make a successful run.
Playbooks do not require them unless the virtual appliance has a specific need (i.e. nsx_ovf_role) or you wish to store your NSX virtual appliance in a vSphere folder, or have a specific resource pool all NSX virtual appliances are going in.

* `nsx_ovf_folder:`
* `nsx_ovf_role:`
* `nsx_ovf_resource_pool:`

## Example (Assumes defaults)

```
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
    - nsx-ovf
```

## Dependencies

None.

