# Ansible Collection - jhampson_dbre.home_assistant

A collection of roles for installing and configuring Home Assistant Supervised on Debian 10

## Roles

### Minimal installation

These roles attempt to implement the strict set of requirements for installing Home Assistant Supervised available [here](https://github.com/home-assistant/architecture/blob/6da4482d171f2ef04de9320d313526653b5818b4/adr/0014-home-assistant-supervised.md)
While every effort has been made to ensure these roles complies with ADR-0014, no guarantee can be made it does now, or in the future. These roles may have software package requirements (e.g. `python3-apt`) that are not specified by ADR-0014. To date these have not caused Home Assistant to report an unsupported installation, but please file a GitHub if you encounter any problems.

[preinstall_config](https://github.com/jhampson-dbre/home_assistant/blob/main/roles/preinstall_config/README.md) - Prerequisite configuration for Home Assistant Supervised installation

### Additional roles

These roles provide additional functionality to secure and enhance the minimal install of Home Assistant Supervised. These roles do not strictly comply with ADR-0014. However, in my own setup, Home Assistant reports the installation is supported. A future update to Home Assistant could change the way that supported installation is reported and detect an unsupported installation, but this is also true for the minimal installation if any of the requirements change.

[harden_os](https://github.com/jhampson-dbre/home_assistant/blob/main/roles/harden_os/README.md) - Enable automated Debian security updates and restrict SSH access
[fail2ban](https://github.com/jhampson-dbre/home_assistant/blob/main/roles/fail2ban/README.md) - Install fail2ban, configure it to blacklist IPs with excessive failed login attempts to Home Assistant, and add the fail2ban integration to Home Assistant