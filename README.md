# Simple Router

**Share your internet access. Share your VPN access.** A Windows tray utility that lets one PC share its network connection with another PC over SSH — built for cases like using an exchange's IP-whitelisted API (Binance/Bybit) from a machine that doesn't have a stable/whitelisted IP of its own.

## The problem it solves

If PC B already has internet or VPN access with a whitelisted/trusted IP, but PC A needs to use that same IP for API calls or browsing, Simple Router creates and maintains an SSH SOCKS5 tunnel from A to B — sharing your VPN access (or plain internet access) from one PC to another. Simple Router only manages the tunnel itself — routing actual application traffic through it is done separately (system proxy setting, a proxifier like SocksCap64, or an app's own proxy config).

## Two roles, one app

On first launch you pick a role — the same installer works as either side:

**Client** (the PC that wants to use another PC's shared access)
- Maintains an `ssh -D` SOCKS5 tunnel with automatic reconnect and exponential backoff
- Tray icon reflects connection state at a glance (disconnected / connecting / connected / error)
- Optional one-click "Set as Windows System Proxy while connected" — automatically points the OS proxy setting at the tunnel on connect and clears it on disconnect, so browsers/apps that respect the system proxy work with zero extra configuration
- Shows a ready-to-copy `socks5h://127.0.0.1:<port>` URL for pointing other apps' own proxy settings at the tunnel
- Built-in SSH key management: generate a new keypair or use an existing one, without ever silently touching your real `.ssh` folder
- Logs every connect/disconnect event with a timestamp

**Server** (the PC sharing its internet/VPN access)
- One-click guided setup: installs and starts Windows' built-in OpenSSH Server, scopes its firewall rule to the local subnet only, and authorizes a Client's public key — all via a background elevated task, so the app itself never needs to run as Administrator
- Manage authorized client keys with friendly names, add/renew/remove them from a simple list
- Shows the PC's available LAN IPs to hand to a Client for setup
- Live SSHD status in the tray and Settings window

## Design notes

- No database — the source of truth for authorized keys is the real OpenSSH `authorized_keys`/`administrators_authorized_keys` files; the app just adds friendly names as local metadata
- Private keys are never written anywhere without an explicit, user-chosen destination folder
- Runs quietly in the tray; closing the window hides it rather than exiting

## Requirements

- Windows 10/11 with the built-in OpenSSH client/server components
- SSH private keys used with the Client role must not be passphrase-protected (the tunnel runs non-interactively)

## Known limitation

Server-side "which client key connected" activity logging isn't available on all Windows/OpenSSH builds — some installations don't expose a way to read sshd's connection log live. Client-side connect/disconnect logging works everywhere.

## Support

If Simple Router's useful to you, consider [buying me a coffee ☕](https://ko-fi.com/bromokun).
