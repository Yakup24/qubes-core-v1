# Changelog

## Personal hardening changes

- Added strict parsing for Qubes firewall rule entries.
- Validated firewall actions, protocols, ports, IP addresses, networks,
  hostnames, ICMP types, special targets, and connected IP lists.
- Made iptables port handling match nftables when a port rule does not specify
  a protocol by generating both TCP and UDP rules.
- Rejected invalid firewall combinations such as ICMP rules with destination
  ports or non-ICMP rules with ICMP types.
- Fixed the `notify-send` environment handling in firewall error reporting.
- Prevented `qubes-vmexec` from attempting to execute an empty command.
- Made Python unit tests less dependent on a full Qubes/Linux desktop runtime.
- Removed live DNS dependence from firewall unit tests.

