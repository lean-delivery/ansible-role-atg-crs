atg_crs
=========
[![License](https://img.shields.io/badge/license-Apache-green.svg?style=flat)](https://raw.githubusercontent.com/lean-delivery/ansible-role-atg-crs/master/LICENSE)
[![Build Status](https://travis-ci.org/lean-delivery/ansible-role-atg-crs.svg?branch=master)](https://travis-ci.org/lean-delivery/ansible-role-atg-crs)
[![Build Status](https://gitlab.com/lean-delivery/ansible-role-atg-crs/badges/master/build.svg)](https://gitlab.com/lean-delivery/ansible-role-atg-crs)

## Summary
--------------

This role installs Oracle ATG Commerce Reference Store. It is designed to serve as both a demonstration of many of the capabilities of Commerce and as a framework to help Commerce site developers to build their own stores more quickly.   


Requirements
--------------

 - Minimal Version of the ansible for installation: 2.5
 - **Supported CRS versions**:
   - 10.x
   - 11.0
   - 11.1
   - 11.2
   - 11.3
   - _lower and higher versions should be retested_
 - **Supported OS**:
   - CentOS
     - 6
     - 7

For more information regarding support matrix please visit <https://support.oracle.com>

ATG platform should be installed preliminarily:
  - lean_delivery.atg_platform


```
For test scenarios atg_crs/requirements.yml is used  
If another roles/versions are required, put requirements.yml to molecule/<scenario_name> and remove in molecule.yml lines  
  options:  
    role-file: requirements.yml
```


Role Variables
--------------

  - `crs_version` - Commerce Reference Store version
  - `transport` - artifact source transport  
     Available:
      - `web` - fetch artifact from custom web uri
      - `local` - local artifact

  - `transport_web` - URI for http/https artifact  e.g. "http://my-storage.example.com/V861211-01.zip"
  - `transport_local` - path for local artifact e.g. "/tmp/V861211-01.zip"

  - `download_path` - local folder for downloading artifacts  
    default: `/tmp`

  - `dynamo_root` - path to installed ATG Platform  
    default: `/opt/atg/ATG`


Example Playbook
----------------

### Installing ATG Commerce Reference Store 11.3 from local:
```yaml
- name: "Install CRS 11.3 from local"
  hosts: all

  roles:
    - role: lean_delivery.java
      java_major_version: 7
      java_minor_version: 80
      transport: "local"
      transport_local: "/tmp/jdk-7u80-linux-x64.tar.gz"
    - role: lean_delivery.jboss
      transport: "local"
      transport_local: "/tmp/jboss-eap-6.1.0.zip"
    - role: lean_delivery.atg_platform
      transport: "local"
      transport_local: "/tmp/V861209-01.zip"
    - role: lean_delivery.atg_crs
      crs_version: "11.3"
      transport: "local"
      transport_local: "/tmp/V861211-01.zip"


  vars:
    atg_version: "11.3"
    dynamo_root: "/opt/atg/ATG{{ atg_version }}"
```

### Installing ATG Commerce Reference Store 10.2 from local:
```yaml
- name: "Install CRS 11.3 from web"
  hosts: all

  roles:
    - role: lean_delivery.java
      java_major_version: 7
      java_minor_version: 80
      transport: "web"
      transport_web: "/tmp/jdk-7u80-linux-x64.tar.gz"
    - role: lean_delivery.jboss
      transport: "web"
      transport_web: "/tmp/jboss-eap-6.1.0.zip"
    - role: lean_delivery.atg_platform
      transport: "web"
      transport_web: "/tmp/V861209-01.zip"
    - role: lean_delivery.atg_crs
      crs_version: "11.3"
      transport: "web"
      transport_web: "http://my-storage.example.com/V861211-01.zip"


  vars:
    atg_version: "11.3"
    dynamo_root: "/opt/atg/ATG{{ atg_version }}"
```


## License

[Apache License 2.0](https://raw.githubusercontent.com/lean-delivery/ansible-role-atg-crs/master/LICENSE)

## Authors

[Lean Delivery team](team@lean-delivery.com)
