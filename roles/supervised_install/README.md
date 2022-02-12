supervised_install
=========

Install Home Assistant Supervised on Raspberry Pi 4 running Debian 11 (bullseye).

Requirements
------------

Python Packages:

- docker

OS Packages:

- python3-apt
- debconf
- debconf-utils

Role Variables
--------------

Variables used from fact gathering

- ansible_pkg_mgr: Used to validate that apt is available, since it is used by this role to install OS packages

Variables in `defaults/main.yml` with default values shown

The variables below are specify to the supervised_install role

```yaml
# Install the requirements for the role listed above.
# The role will error if the requirements are installed,
# but potentially this could make you Home Assistant Supervised
# "unsupported" since it is not required by
# Home Assistant. To maintain "full support", these requirements
# can be manually uninstalled if you are done using this role
supervised_install_ansible_requirements: true

# Number of seconds the homeassistant-supervised deb package installation
# can run before considered to be failed due to timeout
supervised_install_deb_timeout: 600

# The homeassistant-supervised installer may prompt for the machine type.
# The default response for silent install can be configured.
#
# Allowed values in homeassistant-supervised.deb are:
# generic-x86-64, odroid-c2, odroid-n2, odroid-xu, qemuarm, qemuarm-64,
# qemux86, qemux86-64, raspberrypi, raspberrypi2, raspberrypi3, raspberrypi4,
# raspberrypi3-64, raspberrypi4-64, tinker, khadas-vim3r
machine: raspberrypi4-64
```

Dependencies
------------

1. geerlingguy.docker - Used to install Docker CE

The variables below are used by the [geerlingguy.docker](https://github.com/geerlingguy/ansible-role-docker) role. The default is for Raspberry Pi 4 running Debian 64-bit. For other use cases and options, please refer to the geerlingguy.docker README

```yaml
# vars/main.yml
docker_apt_arch: arm64
docker_install_compose: false
```

Example Playbook
----------------

```yaml
# Run the playbook from remote host to Rapsberry Pi 4 running Debian 11 64-bit
- hosts: pi
  become: yes
  force_handlers: true
  roles:
    - role: jhampson_dbre.supervised_install
```

```yaml
# Run the playbook locally in a Debian 11 VM with Ansible installed, running in Hyper-V on Windows
- hosts: localhost
  become: yes
  force_handlers: true
  roles:
    - role: jhampson_dbre.supervised_install
      vars:
        machine: qemux86-64
        docker_apt_arch: amd64
```

License
-------

MIT

Author Information
------------------

@jhampson-dbre
