# Ansible Collection - jhampson_dbre.home_assistant

A collection of roles for installing and configuring Home Assistant Supervised on Debian 10

**WARNING:** The roles in this collection can make changes to Home Assisant's configuration.yaml and restart Home Assistant. As recommended before making any changes to Home Assisant, ensure you have a good snapshot of your current configuration.

## Roles

### Minimal installation

These roles attempt to implement the strict set of requirements for installing Home Assistant Supervised available [here](https://github.com/home-assistant/architecture/blob/6da4482d171f2ef04de9320d313526653b5818b4/adr/0014-home-assistant-supervised.md).
While every effort has been made to ensure these roles complies with ADR-0014, no guarantee can be made it does now, or in the future. These roles may have software package requirements (e.g. `python3-apt`) that are not specified by ADR-0014. To date these have not caused Home Assistant to report an unsupported installation, but please file a GitHub if you encounter any problems.

1. [preinstall_config](https://github.com/jhampson-dbre/home_assistant/blob/main/roles/preinstall_config/README.md) - Prerequisite configuration for Home Assistant Supervised installation

### Additional roles

These roles provide additional functionality to secure and enhance the minimal install of Home Assistant Supervised. These are roles I use myself and do not comply with ADR-0014.

1. [harden_os](https://github.com/jhampson-dbre/home_assistant/blob/main/roles/harden_os/README.md) - Enable automated Debian security updates and restrict SSH access
1. [fail2ban](https://github.com/jhampson-dbre/home_assistant/blob/main/roles/fail2ban/README.md) - Install fail2ban, configure it to blacklist IPs with excessive failed login attempts to Home Assistant, and add the fail2ban integration to Home Assistant
1. [install_hacs](https://github.com/jhampson-dbre/home_assistant/blob/main/roles/install_hacs/README.md) - Install the [Home Assistant Comunity Store](https://hacs.xyz/), a marketplace of community-contributed custom components for Home Assistant