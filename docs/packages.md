# Ansible Role: Simple Package Installer
This role is a simple interface to the `ansible.builtin.package` module to easily add/remove packages based on a list.

## Requirements
This should work on anything that the `ansible.builtin.package` module works on and supports.

## Variables
### `packages_install_list`
Array containing strings of package names to install.

### `packages_remove_list`
Array containing strings of package names to remove.

## Usage
After adding one of the lists to a host/group/etc variable file, just include the role, e.g.:
```
- name: include simple package installer
    import_role:
      name: sedunne.simple.packages
```
