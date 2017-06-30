# Borg backup role

This roles installs Borg backup on backupservers and clients. The role contains a wrapper-script 'borg-backup' to ease the usage on the client. Supported options include borg-backup info | init | list | backup | mount. Per default automysqlbackup will run as pre-backup command.


## Required variables

Define a group backupservers in your inventory with one or multiple hosts. The default location where the backups will be saved is /var/backup/repos/.
```
infra:
[backupservers]
backup1.fiaas.co
```

group\_vars/all.yml:
```
backupservers:
  - backup1.fiaas.co
```
Contains the list of server you want to use on a certain client.
Allows to override backup servers on group or host level.

Define a borg\_passphrase for every host.
host\_vars\client1:
```
borg\_passphrase: Ahl9EiNohr5koosh1Wohs3Shoo3ooZ6p
```

*Make sure to check the configured defaults for this role, which contains the list of default locations being backed up in backup_include.* Override this in your inventory where required.

## Usage

Configure Borg on the server and on a client:
```
ansible-playbook -i inventory/test playbooks/backup.yml -l backup1.fiaas.co
ansible-playbook -i inventory/test playbooks/backup.yml -l client1.fiaas.co
```

## Further reading
https://borgbackup.readthedocs.io/en/stable/