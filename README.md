# Ansible Collection - cadair.sanoid

## Sanoid

Sanoid takes and manages snapshots, it has a toml config file specifying one or more datasets and one or more templates 

## Syncoid

### Design Notes

Syncoid has a source and a sink (where you replicate data from the source to the sink), but you can do this in either push (where the source ssh's to the sink) or pull (where the sink ssh's to the source).

Tasks:

* Make user accounts on the source and the sink.
* Configure zfs permissions on the source and the sink. [zfs_delegate_admin](https://docs.ansible.com/ansible/latest/collections/community/general/zfs_delegate_admin_module.html)
  - source gets the following permissions:
    - send
    - snapshot
    - hold
  - sink gets the following permissons:
    - compression
    - mountpoint
    - create
    - mount
    - receive
    - rollback
    - destroy
* Add the ssh key of the initiator to the passive machine.
  - Generate a keypair on the controller?
  - Copy the required key parts to hosts dependent on push/pull.
* Add a cron on initator to run syncoid with `--no-privilege-escalation`.
* Add an option to not configure the source for a pull backup, i.e. Drew gives me an ssh key and I pull the backup.

See rsnapshot debops role for inspiration on ssh key delegation.
https://github.com/debops/debops/blob/master/ansible/roles/rsnapshot/tasks/main.yml#L87-L162
https://matrix.to/#/%23debops%3Amatrix.org/%247cWBX_Uhyt-lvdHC8YLlcKOWwPujMRm_lBfDf6rSfWA?via=cadair.com&via=libera.chat&via=half-shot.uk&via=matrix.org
