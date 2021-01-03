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

## Usage
By default, just including the role will setup the following:
1. Enable UFW
2. Allow all incoming traffic to port 22
3. Set the default "incoming" and "routed" policies to "reject"
4. Set the default "outgoing" policy to "allow"

Defining your own rules will override the default of allowing port 22, so be careful not to lock yourself out.

```
- name: include firewall
  import_role:
    name: sedunne.simple.ufw
```
