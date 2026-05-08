# Personal Qubes Core Agent Fork

This is a hardened personal fork of `qubes-core-agent-linux`.

The project still follows the original Qubes OS agent layout, but this copy is
tuned for easier local inspection, safer firewall rule handling, and more
deterministic tests outside a full Qubes VM.

## What Changed

- Firewall rules are parsed more strictly before they are translated into
  iptables or nftables input.
- Rule values such as protocols, ports, IP networks, hostnames, ICMP types, and
  special targets are validated early.
- Connected IP values are validated before being inserted into nftables or
  iptables commands.
- The firewall notification path now passes a real environment to
  `notify-send`, including a default `DISPLAY=:0`.
- Optional runtime dependencies such as `python-daemon`, `qubesdb`, `gi`, and
  `pyxdg` no longer break import-only unit tests on a normal development
  machine.
- The desktop-entry tests can run with a small local parser fallback when
  `pyxdg` is not installed.
- Firewall tests no longer depend on live DNS answers.

## Test

From this directory:

```sh
python -m unittest discover -p "test_*.py" -v
```

The full Qubes runtime still needs the normal system dependencies when the
agent services are actually executed inside a VM.

## Development Notes

See `CHANGELOG.md` for the fork-specific hardening work and `SECURITY.md` for a
short review checklist before publishing or testing this inside a VM.

## Notes

This repository contains security-sensitive VM agent code. Keep behavior
changes small, test them, and review firewall/RPC changes with extra care
before using them in a real Qubes environment.
