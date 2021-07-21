# Ansible Role: Wireguard
This role installs and does basic Wireguard interface and peer configuration. Note that this role is *not* intended to be a "turn-key" VPN solution, and just aims to install and setup Wireguard. Additional firewall and/or networking work may be required for your setup. 

At the very least, you'll need to manually give the `wg0` interface an IP address, as no other networking configuration is done after bringing the interface up. Additionally, there is no effort made by the module to persist the Wireguard interface, so this will need to be managed externally based on the system (and network manager) you're targeting.

There's also a slight "gotcha" if you apply the role to a host back-to-back without gathering facts between each run (e.g. using fact-caching). The role will try to create the `wg0` interface on a second run, before the facts have updated, since the `ansible_interfaces` fact won't include the `wg0` interface yet. Clearing the cache/re-gathering facts should resolve this and let that task properly get skipped.

## Requirements
Systems using a Linux kernel `5.6` or greater *should* have the module available by default, and only need a package in an available repository source that supplies the `wg` program (typically called 'wireguard-tools'on Deb-based).

Systems not using the `5.6` or greater Linux kernel need both the "tools" package mentioned above, as well as a package that provides the necessary module/driver for Wireguard (typically just called 'wireguard' on Deb-based).

## Variables
### `wireguard_listenport`
string telling the wg0 interface what port (udp) it should listen on

### `wireguard_packagename` and `wireguard_toolspackagename`
strings that name the packages that provide the Wireguard driver/module and tools, respectively

### `wireguard_peerlist`
list of hashes describing the peers allowed to connect to the wg0 interface. Format should look like the following:

```
wireguard_peerlist:
  - name: 'samsquanch' ## string, used to identify the peer sections in the config, and not actually part of Wireguard
    public_key: '<public key from peer>' ## string, can be found in the wireguard client you're using
    allowed_ips: ['10.0.0.40/32'] ## list of strings, usually just the VPN network IP address of the peer (client) that you're describing
```

## Usage
To install and do a basic setup of Wireguard with no peers, just include the role, e.g.:

```
- name: include simple wireguard role
    import_role:
      name: sedunne.simple.wireguard
```

This will setup a `wg0` interface, listening on udp port '51820' but missing an IP address (needs to set manually), and generates the necessary private/public keys for the interface. Peers can be added via populating the `wireguard_peerlist` variable.
