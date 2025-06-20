# Ansible role for installing Proxmox VE on Debian

> WARNING: Currently this role is WIP!

This role aims to install Proxmox VE on an (blank) Debian installation.  
It is meant to be run on top of this role: [ansible-zfs_on_root](https://github.com/karigeo/ansible-zfs_on_root)

Usage is pretty straight forward and the installation follows the official How-To (https://pve.proxmox.com/wiki/Install_Proxmox_VE_on_Debian_12_Bookworm).

As an optional step (turned on by default) there is the possibility to add entries into `/etc/pve/storage.cfg` as this file will not exist after an installation via packages and it will not be automatically filled with the storage configuration created during system setup.

## Requirements

Fresh Debian 12 installation with networking configured to a static IP.
Best to use [ansible-zfs_on_root](https://github.com/karigeo/ansible-zfs_on_root) to setup the system.

## Role Variables

The available role variable will be listed below together with their default values (defined in `defaults/main.yml`)

```yaml
debug: false
```
Controls whether additional debug output should be shown or not.

```yaml
define_storage_locations: true
```
Controls if `/etc/pve/storage.cfg` should be edited. If it does not exist, it will be created.

```yaml
storage_config:
  - name: local
    type: dir
    path: /var/lib/vz
    content: iso,vztmpl,backup
    shared: 0
```
List of dictionaries to build `storage.cfg` from. Follows the syntax of the config file as described here: https://pve.proxmox.com/wiki/Storage
