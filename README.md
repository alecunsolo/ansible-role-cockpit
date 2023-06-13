[![build status](https://github.com/alecunsolo/ansible-role-cockpit/actions/workflows/ci.yml/badge.svg)](https://github.com/alecunsolo/ansible-role-cockpit/actions/workflows/ci.yml)
[![pre-commit](https://img.shields.io/badge/pre--commit-enabled-brightgreen?logo=pre-commit)](https://github.com/pre-commit/pre-commit)

Ansible Role: cockpit
=========

A role to install [cockpit](https://cockpit-project.org/) on a machine.

Requirements
------------

For the installation of the [45Drives](https://github.com/45Drives/cockpit-zfs-manager.git) component `git` and `rsync` are needed.

Role Variables
--------------

```yaml
cockpit_main_package: cockpit
cockpit_storage_package: cockpit-storaged
cockpit_podman_package: cockpit-podman
cockpit_machines_package: cockpit-machines
cockpit_service: cockpit.socket

cockpit_zfs_manager_repo: https://github.com/45Drives/cockpit-zfs-manager.git
```
Self-explanatory variables defined in (vars/main.yml)[vars/main.yml].
 ```yaml
cockpit_storage_enabled: true
cockpit_podman_enabled: false
cockpit_machines_enabled: false
cockpit_zfs_enabled: false
```
Cockpit packages to be installed.

```yaml
cockpit_ipa_cert: false
```
Whether to attempt to get TLS certificate from IPA server or not.

```yaml
cockpit_override_systemd: false
cockpit_override_src: cockpit-default-override.socket.j2
```
This parameters are used to override the system provided `systemd` unit (for example to listen only on one interface). The provided template is empty: to actually override the unit you need to bring your own template.

Dependencies
------------

None.

Example Playbook
----------------
```yaml
---
- hosts: all
  vars:
    cockpit_storage_enabled: true
    cockpit_podman_enabled: false
    cockpit_machines_enabled: true
    cockpit_zfs_enabled: true
    cockpit_override_src: my_custom_systemd_override.j2
    override_param_1: my_value
  tasks:
    - name: Include cockpit.
      ansible.builtin.include_role:
        name: alecunsolo.cockpit
```

License
-------

MIT

Notes
-----

Testing with molecule is ~~stolen from~~ heavily inspired by [Jeff Geerling](https://www.jeffgeerling.com/). Watch [his video](https://youtu.be/FaXVZ60o8L8) (and the other ones as well).
