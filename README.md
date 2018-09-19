# Ansible Role: GlusterFS with VDO Data Reduction for EL Linux

Installs and configures GlusterFS with VDO on Linux.

## Requirements

For GlusterFS to connect between servers, TCP ports `24007`, `24008`, and `24009`/`49152`, and TCP/UDP port `111` must be open. You can open these using whatever firewall you wish (firewall-cmd etc.).

Only on EL 7.5 and above! Ship with RHEL 7.5 as an out-of-tree module!

Basic installation and Gluster/VDO Setup, no Brick / Volume Mounts. Ansible includes the [`gluster_volume`](https://docs.ansible.com/gluster_volume_module.html) module to ease the management of Gluster volumes.

VDO information you will find here: [`dm_vdo`](https://github.com/dm-vdo), and here: [`redhat_vdo_devel`](https://www.redhat.com/mailman/listinfo/vdo-devel)!

VDO - is a Linux device mapper driver that provides deduplication and compression (https://de.slideshare.net/GlusterCommunity/data-reduction-for-gluster-with-vdo)
• VDO has two kernel modules that work together to provide data efficiency 
• The kvdo module - controls block layer and compression 
• The uds module - maintains deduplication index and provides advice 
• VDO can be used under:
 • Block storage 
 • File storage - (Gluster!)
 • Object storage • Utilities: 
 • vdo - Manage VDO volumes (create, remove, modify) and view configurations 

## Role Variables

    vdo_create:
    - lv_name: gluster_vdosd
      disk: /dev/sdc
      logical_size: 128G
      filesystem: xfs
      mount_options: rw,inode64,noatime,nouuid,discard
      mount: /gluster_bricks/vdosd
      rebalance: no
      replicas: 3
      gluster_server1: gluster_ip1
      gluster_server2: gluster_ip2
      gluster_server3: gluster_ip3

    vdo_remove:
    - lv_name: gluster_vdosd
      mount: /gluster_bricks/vdosd

## Dependencies

# Remove Procedure will only remove vdo volume because the ansible gluster_volume_module do not support remove option at this time.
  Feature Request and State > https://github.com/ansible/ansible/issues/38174

## Example Playbook

    - hosts: server
      roles:
        - mthkunze.vdo.glusterfs


## License

MIT / BSD

## Author Information

[Martin Kunze](https://www./)
