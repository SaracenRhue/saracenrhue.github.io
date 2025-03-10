---
title: Tailscale
date: 2024-10-28 +0000
categories: [linux,networking,vpn]
tags: [linux,networking,tailscale,vpn,documentation,wireguard]
---

## Overview

Tailscale is is a VPN based on Wireguard and allows you to connect your devices in a wireguard mesh network.

## Installation

```bash
curl -fsSL https://tailscale.com/install.sh | sh
```

## Usage 

```bash
tailscale up
```

### Flags 

- `--ssh` - Enable the Tailscale SSH server to eliminate the need for managing SSH keys manually.
- `--advertise-routes=192.0.2.0/24` - Advertise routes so you can access devices over Tailscale where it cant be installed directly.
- `--accept-routes` - Accept routes to other Tailscale nodes.
- `--exit-node` - Use a specific node as the exit node for all traffic.

> If you use routes or exit nodes you need to confirm this in the route settings of the device in the tailscale admin console.
{: .prompt-tip }

Full documentation can be found [here](https://tailscale.com/kb/1017/install).