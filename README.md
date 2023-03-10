# Ansible Collection - dholzer.vmware_usm

Documentation for the collection.

# usm.yml
```
usm:
  deployment:
    vce:
      hostname: 'base01-vce-01.vcloud24.net'
      username: 'administrator@vsphere.local'
      password: 'VMwareVCE1.'
    
    ova: 'vCloud-Usage-Meter-Agent-4.6.0.0-20554128.ova'

    datacenter: 'base01'
    folder: '/vcd01'
    # to cluster 'base01'
    # to resource pool 'base01/Resources/vcd01'
    cluster: 'base01/Resources/01-usm'

    disk_provisioning: 'thin'
    datastore: 'qnap-ts879 vmw_vsphere'

    network: 'base01-0101mgmt'
  netmask_cidr: 26
  gateway: 172.16.0.1
  dns: 172.16.0.1
  ip: 172.16.0.25

  domain: "vcloud24.net"
  searchpath: "vcloud24.net"
  
  root_password: 'VMwareUSM1.'
  usagemeter_password: 'VMwareUSM1.'
  umauditor_password: 'VMwareUSM1.'
  #retain_usage_data: True
  #offline_mode: False
  #offline_token: ''
  hostname: psrv01usm001.vcloud24.net
  check_pattern: "VMware vCloud Usage Meter 4.6"


  product:
    - host: "lab01-vce-01.vcloud24.net"
      productType: 'vCenter'
      port: 443
      user: "administrator@vsphere.local"
      password: "VMwareVCE1."
      externalSSO: false
      srmMetered: false
      k8sMetric: "vRAM"
      state: present

    - host: "lab01-ntm-01.vcloud24.net"
      productType: 'NSX-T'
      port: 443
      user: "admin"
      password: "VMwareNSX1.."
      state: present

    - host: "psrv01vcd001.vcloud24.net"
      productType: 'VCD'
      port: 443
      user: "administrator@system"
      password: "VMwareVCD1."
      state: present

    - host: "psrv01cam001.vcloud24.net"
      productType: 'VCAV'
      port: 443
      user: "root"
      password: "Swisscom.01"
      state: present

#    - host: "psrv01ops001.vcloud24.net"
#      productType: 'VROPS'
#      port: 443
#      user: "root"
#      password: "Swisscom.01"
#      state: present
  ```
# site.yml
```
---
- hosts: localhost
  gather_facts: false
  collections:
    - swisscom.vmware_usm
  
  roles:
    - usm_deploy
    - usm_api_session
    - usm_config_product
```