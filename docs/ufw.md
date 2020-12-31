# Ansible Role: Simple UFW
This role is a simple interface to manage UFW on Ubuntu systems.

## Requirements
Currently supported releases are:

* 20.04 (focal)

## Variables
### `firewall_ufw_rules`
List of hashes containing 3 keys: "rule", "port", and "proto". Eg: `{ rule: "allow", port: "22", proto: "tcp" }`

### `firewall_ufw_delete`
Same format as `firewall_ufw_rules`, except this list should only contain entries that you want to remove from the target system (removing it from the rules list won't remove it on the host).

### `firewall_ufw_policies`
Dict of default policies and their state. Eg:
```
  incoming:
    policy: "reject"
    route: "no"
```
