os_agent_auto_update
=========

Schedule ansible-playbook to check for and install OS Agent updates with cron

Requirements
------------

- Ansible must be installed on the remote host to run the auto update playbook from cron. The role will complete successfully without Ansible being installed, but the cron job will not run successfully. By default, the role will automatically do a user install of ansible with pip.
- A playbook is copied to the remote host that is scheduled in cron to check for and install OS Agent updates. This playbook has a task with `become: true`, so the user runs the schedule should have passwordless sudo configured to run non-interactively.

Role Variables
--------------

The following varaibles are defined in `defaults/main.yml`

```yaml
# The path that the automatic update playbook will be copied to for scheduling
os_agent_auto_update_playbook_dir: /home/homeassistant/playbooks

# Install ansible on the remote host so that the update playbook can run in cron. Set to false to you already have ansible installed, or need a specific Ansible version.
os_agent_auto_update_install_ansible: true
```

Dependencies
------------

none

Example Playbook
----------------

```yaml
- hosts: pi
  roles:
    - name: jhampson_dbre.home_assistant.os_agent_auto_update
```

License
-------

MIT

Author Information
------------------

@jhampson-dbre