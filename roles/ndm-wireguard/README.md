# ivansible.ndm_wireguard

[![Github Test Status](https://github.com/ivansible/ndm-wireguard/workflows/Molecule%20test/badge.svg?branch=master)](https://github.com/ivansible/ndm-wireguard/actions)
[![Travis Test Status](https://travis-ci.org/ivansible/ndm-wireguard.svg?branch=master)](https://travis-ci.org/ivansible/ndm-wireguard)
[![Ansible Galaxy](https://img.shields.io/badge/galaxy-ivansible.ndm__wireguard-68a.svg?style=flat)](https://galaxy.ansible.com/ivansible/ndm_wireguard/)

This role configures Wireguard interfaces on Keenetic NDMS using RCI HTTP API.
A separate network interface is created for each remote peer.


## Requirements

None


## Variables

Main variables are listed below:

    ndm_wg_addr: 10.1.1.1/24
IP address and netmask to assign to Wireguard interface.
Currently it is shared between peers,
in future it will become a per-peer setting.

    ndm_wg_host: ~
Reserved for future use.

    ndm_wg_port: 0
Wireguard listening port (or zero if not listening).

    ndm_wg_key: ~
    ndm_wg_pub: ~
    ndm_wg_psk: ~
Private, public and preshared keys of the local Wireguard node.
Private key is required, while public key is purely informational.
Preshared key is optional.

    ndm_wg_mtu: 1420
Allows to force MTU on interface.

    ndm_wg_keepalive: 0
If non-zero, enables persistent keepalive in seconds.

    ndm_wg_peers: []
This is an array of records, where each record describes a remote
Wireguard peer and has the following fields:
  - `name` -- required peer name (peer is skipped if name is empty);
  - `active` -- optional boolean flag, defaults to true;
  - `key` -- peer private key, purely informational;
  - `pub` -- peer public key, required;
  - `psk` -- preshared key, optional;
  - `ips` -- allowed IPs, list of ip/mask pairs;
  - `host` -- peer IP address, required;
  - `port` -- port of endpoint, required.


## Tags

- `ndm_wg_all` -- all tasks


## Dependencies

None


## Example Playbook

    - hosts: keenetic
      roles:
         - role: ivansible.ndm_wireguard
           ndm_wg_key: abc123xyz


## License

MIT


## Author Information

Created in 2020 by [IvanSible](https://github.com/ivansible)
