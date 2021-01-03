# Ansible Role: Simple Canonical Livepatch
This role is a simple interface to setup the Canonical Livepatch snap for Ubuntu servers.

## Requirements
Currently supported releases are:

* 20.04 (focal)

## Variables
### `canonical_livepatch_token`
String containing the livepatch token for the Canonical account you're using.

## Usage
After defining the token variable, just include the role and the snap will be installed and started:
```
- name: include simple livepatch
    import_role:
      name: sedunne.simple.livepatch
```
