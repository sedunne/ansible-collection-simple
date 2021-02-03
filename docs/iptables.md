# Ansible Role: Simple iptables
This role is a simple interface to manage iptables on Ubuntu systems. It's rather heavy-handed, and based on the stateful firewall configuration from the [Arch wiki](https://wiki.archlinux.org/index.php/Simple_stateful_firewall). It is not meant to support complicated chains or rules, and you might run into issues doing so.

## Requirements
Currently supported releases are:

* 20.04 (focal)

## Variables
### `iptables_rules`
List of strings containing iptables rules in the format that they'd appear with via `iptables-save`. Eg:
```
iptables_rules:
  - "-A TCP -p tcp --dport 22 -j ACCEPT"
  - "-A FORWARD -i docker0 -o eth0 -j ACCEPT"
  - "-A FORWARD -i eth0 -o docker0 -j ACCEPT"
```

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
