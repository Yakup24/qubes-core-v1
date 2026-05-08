# Personal Qubes Core Agent Fork

[![Tests](https://github.com/Yakup24/qubes-core-v1/actions/workflows/tests.yml/badge.svg)](https://github.com/Yakup24/qubes-core-v1/actions/workflows/tests.yml)
[![License: GPL v2 or later](https://img.shields.io/badge/License-GPL_v2_or_later-blue.svg)](LICENSE)

This is a hardened personal fork of `qubes-core-agent-linux`.

The project still follows the original Qubes OS agent layout, but this copy is
tuned for easier local inspection, safer firewall rule handling, and more
deterministic tests outside a full Qubes VM.

License: GNU General Public License v2.0 or later.

## Upstream Base

This repository is based on QubesOS/qubes-core-agent-linux.

Upstream project:
https://github.com/QubesOS/qubes-core-agent-linux

This fork focuses on:

- stricter firewall rule validation
- safer handling of rule inputs
- deterministic unit tests outside a full Qubes VM
- small maintainability improvements

This is not an official Qubes OS component.

## Warning

This repository contains security-sensitive VM agent code. Do not use this fork
in a production or daily Qubes environment without reviewing the changes,
running the test suite, and testing inside a disposable Qubes VM.

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

Keep behavior changes small, test them, and review firewall/RPC changes with
extra care before using them in a real Qubes environment.
