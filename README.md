# Ansible "Simple" Collection
This collection is intended to house the small roles I've created to do various things.

Roles here are not meant to be incredibly feature rich or support a wide variety of configurations. Rather, the goal of these roles is just to provide something usable quick, configured in a hopefully-sane way. More featureful roles will be moved into their own repo, and managed more traditionally.

## Included Roles
### iptables
This role sets up a basic iptables-based stateful firewall, with support for filter and nat table rules.

### livepatch
This role installs and configures the Canonical Livepatch snap on Ubuntu systems.

### ufw
This role allows for basic UFW management on Ubuntu systems.

### packages
This role is a very basic interface to the `ansible.builtin.packages` module.

### wireguard
This role installs (if needed) and sets up a Wireguard interface and peer list.

## Docs
The `docs/` directory contains detailed information on the included roles, including their supported platforms and variables.
