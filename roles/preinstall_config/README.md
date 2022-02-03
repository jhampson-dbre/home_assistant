home_assistant.preinstall_config
=========

Prepare Rapsberry Pi 4 running Debian 11 for Home Assistant Supervised installation.

Requirements
------------

This role is intended to run on Raspberry Pi 4 running Debian 11 installed using steps 1.1-1.3 of the [Installing Home Assistant Supervised on a Raspberry Pi with Debian 11](https://community.home-assistant.io/t/installing-home-assistant-supervised-on-a-raspberry-pi-with-debian-11/247116) community guide.

Since Ansible requires SSH to manage machines remotely, it is recommended to activate the root login by editing the sysconfig.txt file and uncomment the root password and the root_authorized_key. Then you should generate an SSH key pair and use the generated public key to paste there.

This role generates SSH keys on the control node for the currently logged in user to remotely manage the Raspberry Pi, so you should run this role from the machine you want to use to for remote management

The following software is required on the control node:

- ssh-keygen

Role Variables
--------------

The following facts are used by this role

```yaml
ansible_default_ipv4['address']: Use to configure static IP in /etc/hosts when `has_reserved_ip == true`
```

Variables in `defaults/main.yml` with default values

```yaml
# non-root user to create on the Home Assistant server
home_assistant_user: homeassistant

# Set this to true if you have a static IP for the Raspberry Pi
# When set to true, set the ipv4 address in /etc/hosts
# When set to false, 127.0.1.1 will be set in /etc/hosts
has_reserved_ip: false
```

Dependencies
------------

None

Example Playbook
----------------

```yaml
# Run the playbook from remote control node to Rapsberry Pi
# and override the default name of the non-root account to create
- hosts: pi
  become: yes
  tasks:
    - name: Prepare Pi for Home Assistant Supervised installation
      import_role:
        name: jhampson_dbre.home_assistant.preinstall_config
      vars:
        home_assistant_user: james
```

License
-------

MIT

Author Information
------------------

@jhampson-dbre
