home_assistant.restore
=========

Restore a full Home Assistant backup

Requirements
------------

`ha` command line utility it required, which should be automatically installed during Home Assistant Supervised installation.

Role Variables
--------------

Required parameters with example values

```yaml
# the name of the backup file to restore
restore_backup_file_name: Full Backup 2022-02-12 03_26_00.tar
```

Optional parameters with example values

```yaml
# directory on the ansible controller where
# the backup file is. If set, the backup file
# will be copied from here to `restore_home_assistant_backup_dir` on the remote home assistant host. Otherwise, the backup file should already exist on the home assistant host.
restore_copy_source_dir: /mnt/c/Users/me/Downloads

# For password-protected backups, the password is required to decrypt the backup
restore_backup_password: myBackupP@ssw0rd
```

Variables in `defaults/main.yml` with default values

```yaml
# path on the home assistant server where
# backups are located
restore_home_assistant_backup_dir: /usr/share/hassio/backup
```

Dependencies
------------

None

Example Playbook
----------------

```yaml
# copy a password protected backup file
# from the ansible controller to the Home Assistant server and restore it
- hosts: pi
  become: yes
  tasks:
    - name: restore home assistant backup
      import_role:
        name: jhampson_dbre.home_assistant.restore
      vars:
        restore_backup_file_name: Full Backup 2022-02-12 03_26_00.tar
        restore_copy_source_dir: /mnt/c/Users/me/Downloads
        restore_backup_password: myBackupP@ssw0rd
```


License
-------

MIT

Author Information
------------------

@jhampson-dbre
