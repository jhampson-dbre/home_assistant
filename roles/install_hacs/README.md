install_hacs
=========

Install the [Home Assistant Community Store](https://hacs.xyz/) in Home Assistant Supervised. Use this role as an alternative to the HACS [install shell script](https://github.com/hacs/install/blob/main/install).

Requirements
------------

- unzip is required on the target host
- The role must be ran as root or as an alternate user with `become: true`

Role Variables
--------------

The following varaibles are defined in `defaults/main.yml`

```yaml
# The path of the home assistant config directory. You should not need to change this for Supervised installation.
ha_path: /usr/share/hassio/homeassistant

# Automatically install software packages listed under requirements
install_hacs_requirements: true
```

Dependencies
------------

none

Example Playbook
----------------

```yaml
- hosts: pi
  roles:
    - name: jhampson_dbre.home_assistant.install_hacs
```

License
-------

MIT

Author Information
------------------

@jhampson-dbre