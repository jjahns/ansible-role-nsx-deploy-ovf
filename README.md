# Ansible Role: nsx-deploy-ovf

## Description

Deploy a NSX-T virtual appliance (OVF/OVA) to a vSphere environment.

## Requirements

* pyVmomi (install via pip)
* pyVim (install via pip)
* ansible (latest release)
* NSX-T (2.2 or higher)

## Role Variables

All variables with default values are located in [defaults/main.yml](defaults/main.yml) and can be overridden. It is recommended that variables be placed at the host_vars level per NSX-T virtual appliance deployed. While playbooks can use a local connection, variables are still in the context of the host(s) referenced in the playbooks using this role.

| Name           | Default Value | Description                        |
| -------------- | ------------- | -----------------------------------|
| `nsx_ovf_vsphere_hostname` | | IP/FQDN of vSphere host (vCenter/ESXI) |
| `nsx_ovf_vsphere_username` | administrator@vsphere.local | vSphere user account to deploy virtual appliance with |
| `nsx_ovf_vsphere_password` | | Password of vSphere user account |
| `nsx_ovf_vsphere_validate_certs` | True | Whether or not to validate vSphere SSL certificates |
| `nsx_ovf_datacenter` | | Datacenter to deploy virtual appliance to |
| `nsx_ovf_cluster` | | Cluster to deploy virtual appliance to |
| `nsx_ovf_datastore` | | Datastore to deploy virtual appliance to |
| `nsx_ovf_networks` | | Key: Value association between OVF network names and vSphere port groups |
| `nsx_ovf_path` | | Absolute path to the OVA/OVF file |
| `nsx_ovf_allow_duplicates` | False | Whether or not to allow deployment of a virtual appliance with the same name as an existing VM |
| `nsx_ovf_deployment_option` | medium | The deployment size of the virtual appliance |
| `nsx_ovf_disk_provisioning` | thin | Type of disk mode to use when deploying the virtual appliance |
| `nsx_ovf_fail_on_spec_warnings` | True | Fail any time there is a specification warning in the deployment |
| `nsx_ovf_vmname` | "{{ inventory_hostname }}" | The name of the VM as it appears in vSphere inventory |
| `nsx_ovf_power_on` | True | Whether or not to power the VM on after deployment |
| `nsx_ovf_enable_ssh` | False | Whether or not to enable SSH for the admin account on the VM |
| `nsx_ovf_enable_root_ssh` | False | Whether or not to enable SSH for the root account on the VM |
| `nsx_ovf_vmhostname` | "{{ inventory_hostname }}" | The hostname of the VM |
| `nsx_ovf_wait` | True | Wait until OVF successfully completes before exiting |
| `nsx_ovf_wait_for_ip_address` | True | Wait until the VM reports a valid IP address using guest tools before exiting |
| `nsx_ovf_ip_address` | | IP address to assign to VM |
| `nsx_ovf_netmask` | | Netmask |
| `nsx_ovf_gateway` | | Gateway |
| `nsx_ovf_dns_servers` | | YAML list of DNS servers |
| `nsx_ovf_domain` | | Domain suffix of VM |
| `nsx_ovf_ntp_servers` | | YAML list of NTP servers |
| `nsx_ovf_password` | | Password of the admin account |
| `nsx_ovf_root_password` | | Password of the root account |
| `nsx_ovf_folder` | | An optional folder location to place the VM at in vSphere |
| `nsx_ovf_role` | | An optional value to specify for VM role, useful if deploying the unified appliance |
| `nsx_ovf_resource_pool` | | An optional resource pool to place the VM at in vSphere |

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
    - nsx-deploy-ovf
```
## License

This project is licened under [BSD-2](https://opensource.org/licenses/BSD-2-Clause) License. See [LICENSE](/LICENSE) for more details.

## Dependencies

None.

