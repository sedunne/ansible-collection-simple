# Ansible Role: Simple iptables
This role is a simple interface to manage iptables on systems. It's rather heavy-handed, and based on the stateful firewall configuration from the [Arch wiki](https://wiki.archlinux.org/index.php/Simple_stateful_firewall). It is not meant to support overly complicated chains or rules, and you might run into issues doing so.

## Requirements
Currently supported systems are:

* Ubuntu 20.04 (Focal)
* Debian 11 (Bullseye)

## Variables
### `iptables4_rules`
List of strings containing iptables v4 rules in the format that they'd appear with via `iptables-save`. Eg:
```
iptables_rules:
  - "-A TCP -p tcp --dport 22 -j ACCEPT"
  - "-A FORWARD -i docker0 -o eth0 -j ACCEPT"
  - "-A FORWARD -i eth0 -o docker0 -j ACCEPT"
```

### `iptables6_rules`
Same as `iptables4_rules`, but for iptables v6.

### `iptables4_rules_nat`
List of strings containing iptables rules similar to `iptables_rules`, but to be applied to the nat table instead.

## Usage
By default, just including the role will setup the following:
1. Install the `iptables-persistent` package
2. Allow all incoming traffic to port 22
3. Enable iptables to start on boot

Defining your own rules will override the default of allowing port 22, so be careful not to lock yourself out.

```
- name: include firewall
  import_role:
    name: sedunne.simple.iptables
```
