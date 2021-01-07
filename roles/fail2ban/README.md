fail2ban
=========

Install and configure fail2ban to block IPs with excessive failed login attempts to Home Assistant Supervised. The fail2ban sensor integration is also added to Home Assistant

This role is based upon this documentation:

[Banning IPs from Home Assistant and SSH](https://kevinfronczak.com/blog/banning-ips-on-homeassistant-and-ssh)
[fail2ban Integration Documentation](https://www.home-assistant.io/integrations/fail2ban/)

**WARNING:** This role will make changes to Home Assisant's configuration.yaml and restart Home Assistant. As recommended before making any changes to Home Assisant, ensure you have a good snapshot of your current configuration.

Requirements
------------

- Home Assistant Supervised installation running on Debian 10
- NGINX Home Assistant SSL proxy add-on should be configured as reverse proxy for Home Assistant
- This role must be ran as root, or as an alternate user with `become: true` set
- Docker SDK for Python: `docker` Python package on the target server
- In Home Assistant's configuration.yaml, any pre-existing entries under `http` or `logger` headings will cause this role to fail. These settings are not defined in configuration.yaml by default, but if you have added any custom configuration under either of these headings, please remove it before running this role and then merge any custom configuration with the entries added by this role.

Role Variables
--------------
The following variables are set in `defaults/main.yml`, with default values shown:

```yaml
# The fail2ban jails that will be configured
# Currently only ssh and Home Assistant jails can be configured.
fail2ban_jails:
  - ssh
  - hass-iptables

# The number of failed log in attempts that will result in a ban
# This number is used for all jails
max_failed_login_attempts: 5
```

The following variables are set in `vars/main.yml`, with example values show. See `vars/main.yml` for the full values:

```yaml
# Properties to set, log path, ports, etc. for each fail2ban jail
fail2ban_properties:
  - section: ssh
    options:
      - option: port
        value: ssh
      - option: filter
        value: sshd
      - option: logpath
        value: /var/log/auth.log
```

Dependencies
------------

None.

Example Playbook
----------------

```yaml
# Configure fail2ban for Home Assistant Supervised
# with 3 failed login attempts resulting in ban
- hosts: pi
  become: true
  roles:
    - role: jhampson_dbre.home_assistant.fail2ban
      vars:
        max_failed_login_attempts: 3
```

License
-------

MIT

Author Information
------------------

@jhampson-dbre
