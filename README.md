# Task 4 — Setup and Use a Firewall

**OS used:** (Ubuntu 22.04 / Windows 10 — choose one)

## Objective
Configure and test basic firewall rules to block Telnet (port 23) and verify connectivity, then restore original settings.

## Steps performed
1. Saved current firewall rules:
   - `ufw status verbose` → `outputs/ufw_status_before.txt`
   - `iptables-save` → `outputs/iptables_rules_before.txt`
   - (Windows) `Get-NetFirewallRule -Direction Inbound` → `outputs/inbound_rules_before.txt`

2. Allowed SSH (port 22) to avoid lockout:
   - `sudo ufw allow 22/tcp` (Linux)
   - `New-NetFirewallRule -DisplayName "Allow SSH Port 22" ...` (Windows)

3. Blocked Telnet (port 23):
   - `sudo ufw deny 23/tcp` (Linux)
   - `New-NetFirewallRule -DisplayName "Block Telnet Port 23" ...` (Windows)

4. Verified the block:
   - `nc -vz localhost 23` or `telnet localhost 23`
   - `Test-NetConnection -ComputerName localhost -Port 23`

5. Restored original state:
   - `sudo ufw delete deny 23/tcp` (Linux)
   - `Remove-NetFirewallRule -DisplayName "Block Telnet Port 23"` (Windows)

## Files included
- `screenshots/` — GUI and test screenshots
- `outputs/` — command outputs and logs
- `scripts/` — (optional) command scripts

## Short summary: how firewall filters traffic
A firewall inspects packet headers (and sometimes connection state) to allow or block traffic based on rules (port, protocol, IP, direction). UFW is a front-end that manages iptables rules (stateful) simplifying common tasks.

