# Simple Router

**Simple Router** is an application designed to share internet or VPN access from a single PC (securly) to multiple other PCs on a local network.

## Common Scenarios Addressed
This application solves the following common networking issues:
1. **Limited Internet Access:** In a local network (whether via Wi-Fi or LAN cable), only one PC has active internet access, while the other connected PCs do not.
2. **Limited VPN Access:** In a local network (whether via Wi-Fi or LAN cable), only one PC has access to a specific VPN, while the other connected PCs do not.

## How It Works
Here is how you can use Simple Router to share your connection:

1. **Server Setup:** Install Simple Router on the PC that already has internet and/or VPN access, and configure it to **Server Mode**.
2. **Client Setup:** Install Simple Router on the other PCs connected to the same local network, and configure them to **Client Mode**.
3. **SSH Authentication:** Each Client PC generates an SSH key. The Client must then provide their **SSH Public Key** to the Server operator so it can be registered and authorized.
4. **Connect and Browse:** Once the Client's SSH public key is successfully registered on the Server, the Client can establish a secure connection to the Server PC. After connecting, the Client users can browse the internet seamlessly and utilize the Server's VPN connection.

## Setup
Download Installer -> [Win Intaller](https://github.com/bromoapp/SimpleRouter_release/releases "Installer")

WIKI -> [How to Setup](https://github.com/bromoapp/SimpleRouter_release/wiki/How-to-Setup "View the setup guide")

## Requirements

- Windows 10/11 with the built-in OpenSSH client/server components
- SSH private keys used with the Client role must not be passphrase-protected (the tunnel runs non-interactively)
- All PCs must run in the same network segment.

## Support

If Simple Router's useful to you, consider [buying me a coffee ☕](https://ko-fi.com/bromokun).
