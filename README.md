# Ansible Collection - jhampson_dbre.home_assistant

A collection of roles for installing and configuring Home Assistant Supervised on Debian 11

**WARNING:** The roles in this collection can make changes to Home Assisant's configuration.yaml and restart Home Assistant. As recommended before making any changes to Home Assisant, ensure you have a good snapshot of your current configuration.

## Roles

### Minimal installation

These roles attempt to implement the strict set of requirements for installing Home Assistant Supervised available [here](https://github.com/home-assistant/architecture/blob/master/adr/0014-home-assistant-supervised.md).
While every effort has been made to ensure these roles complies with ADR-0014, no guarantee can be made it does now, or in the future. These roles may have software package requirements (e.g. `python3-apt`) that are not specified by ADR-0014. To date these have not caused Home Assistant to report an unsupported installation, but please file a GitHub issue if you encounter any problems.

1. [preinstall_config](https://github.com/jhampson-dbre/home_assistant/blob/main/roles/preinstall_config/README.md) - Prerequisite configuration for Home Assistant Supervised installation

1. [supervised_install](https://github.com/jhampson-dbre/home_assistant/blob/main/roles/supervised_install/README.md) - Supported installation of Home Assistant Supervised on Debian 11

### Additional roles

These roles provide additional functionality to secure and enhance the minimal install of Home Assistant Supervised. These are roles I use myself and do not *strictly* comply with ADR-0014. However ADR-0014 states that maintaining and securiting the operating system is the responsibility of the user, and these roles fulfill that requirement without interfering with the Supervised installation.

1. [harden_os](https://github.com/jhampson-dbre/home_assistant/blob/main/roles/harden_os/README.md) - Enable automated Debian security updates and restrict SSH access
1. [fail2ban](https://github.com/jhampson-dbre/home_assistant/blob/main/roles/fail2ban/README.md) - Install fail2ban, configure it to blacklist IPs with excessive failed login attempts to Home Assistant, and add the fail2ban integration to Home Assistant
1. [install_hacs](https://github.com/jhampson-dbre/home_assistant/blob/main/roles/install_hacs/README.md) - Install the [Home Assistant Comunity Store](https://hacs.xyz/), a marketplace of community-contributed custom components for Home Assistant
1. [os_agent_auto_update](https://github.com/jhampson-dbre/home_assistant/blob/main/roles/os_agent_auto_update/README.md) - Configures automatic updates to OS Agent component using `ansible-playbook` scheduled with cron

### Example Playbook

```yaml
---
# Minimal Install
#
# Initial setup connects as root over SSH to create
# a new, non-root account to use going forward.
# After the first run, `ansible_user: root` can be removed
# and the non-root account can be used (e.g. as host_var)
- name: Initial OS setup
  hosts: all
  vars:
    ansible_user: root
  become: yes
  tasks:
    - name: Import preinstall_config role
      import_role:
        name: jhampson_dbre.home_assistant.preinstall_config
      vars:
        has_reserved_ip: true

# Since preinstall_config creates a non-root account with sudo access,
# we can use `become: yes` for privilege escalation
# instead of logging in directly as root.
#
# Use `force_handlers: true` to ensure to ensure any changed services
# are restarted even if an error is encountered before the play ends
- name: Install Home Assistant Supervised and Requirements
  hosts: all
  become: yes
  force_handlers: true
  roles:
    - name: jhampson_dbre.home_assistant_supervised

# Extras
- name: Security Hardening and enhancements
  hosts: all
  become: yes
  force_handlers: true
  roles:
    - name: jhampson_dbre.home_assistant.harden_os
    - name: jhampson_dbre.home_assistant.fail2ban
    - name: jhampson_dbre.home_assistant.install_hacs
    - name: jhampson_dbre.home_assistant.os_agent_auto_update
```