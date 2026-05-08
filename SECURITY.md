# Security Notes

This project contains VM agent code and should be treated as
security-sensitive.

## Local Review Checklist

- Run the Python unit tests before publishing changes.
- Review firewall rule parsing changes carefully.
- Avoid inserting unvalidated QubesDB values into shell, nftables, iptables, or
  RPC command inputs.
- Preserve the original GPL license and upstream copyright notices.
- Test service changes inside a disposable or non-critical Qubes VM before
  using them in a daily environment.

## Supported Scope

This fork focuses on safer parsing, deterministic tests, and maintainability.
It does not claim upstream Qubes OS support unless changes are submitted and
accepted upstream.
