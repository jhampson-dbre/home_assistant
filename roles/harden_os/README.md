harden_os
=========

Improve security of Debian 11 OS running Home Assistant Supervised on Raspberry Pi 4

This role can perform the following hardening:

1. Harden SSH

  - Disable root SSH login
  - Disable SSH password authentication
  - Only allow SSH key authentication

1. Enable Automatic Security Updates

  - Install and configure unattended-upgrades


Requirements
------------

This role must be ran as the root user or with `become` enabled.

Additional considerations:

- Harden SSH

  You should ensure that you have a non-root user with sudo priviledges and an SSH key configured before running this role. This can be completed accomplished by running the `jhampson_dbre.home_assistant.preinstall_config` role that is available in the collection.

- Automatic Security Updates

  If automatic reboots are enabled, ensure the time is set correctly on the Raspberry Pi to ensure reboots happen at the expectd time.

Role Variables
--------------

The following variables are set in `defaults/main.yml`

```yaml
# Lock down SSH, including disabling SSH root log in
harden_ssh: true

# Configure automatic installation of security updates
enable_automatic_security_updates: true

## Automatic Security Patching options

# Reboot automatically if reboot is required for installed patches
enable_patching_reboot: "true"

# The time to reboot at if automatic reboot is enabled
patching_reboot_time: "04:00"
```

Dependencies
------------

none

Example Playbook
----------------

```yaml

- hosts: pi
  roles:
     - role: jhampson_dbre.home_assistant.harden_os
```

License
-------

MIT

Author Information
------------------

@jhampson-dbre
