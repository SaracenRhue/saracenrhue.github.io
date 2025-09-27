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
- `--qr` - show a QR code to complete the login via phone.

> If you use routes or exit nodes you need to confirm this in the route settings of the device in the tailscale admin console.
{: .prompt-tip }

Full documentation can be found [here](https://tailscale.com/kb/1017/install).

## IP6 Subnet Routing


### Step 1: Generate IPv6 Subnet Route
- **Command**: Generate an IPv6 route for the IPv4 subnet with a unique site ID (0–65535).
  ```
  tailscale debug via <site-id> <ipv4-subnet>
  ```
  **Example**: For `192.168.178.0/24` with site ID `0`:
  ```
  tailscale debug via 0 192.168.178.0/24
  ```
  **Output**: `fd7a:115c:a1e0:b1a::c0a8:b200/120`
  - `fd7a:115c:a1e0:b1a`: Fixed 64-bit Tailscale prefix.
  - `::`: Site ID `0` (empty translator identifier).
  - `c0a8:b200`: Hex for `192.168.178.0`.
  - `/120`: Subnet mask for `/24`.

### Step 2: Advertise the Route
- **Command**: Advertise the IPv6 route on the subnet router.
  ```
  tailscale set --advertise-routes=<ipv6-route>
  ```
  **Example**:
  ```
  tailscale set --advertise-routes=fd7a:115c:a1e0:b1a::c0a8:b200/120
  ```
- **Approve Route**: In the Tailscale admin console (https://login.tailscale.com/admin), go to **Machines**, find the subnet router, and approve the route.

### Step 3: Get IPv6 Address for a Device
- **Convert IPv4 to IPv6**:
  - For `192.168.178.1`, convert to hex: `192=c0`, `168=a8`, `178=b2`, `1=01` → `c0a8:b201`.
  - Append to prefix and site ID: `fd7a:115c:a1e0:b1a::c0a8:b201`.
- **MagicDNS Name** (if enabled): `<Q-R-S-T>-via-<site-id>`
  - Example: `192-168-178-1-via-0`.

### Step 4: Access Web UI
- **Using IPv6**:
  - HTTP (port 80): `http://[fd7a:115c:a1e0:b1a::c0a8:b201]`
  - HTTPS (port 443): `https://[fd7a:115c:a1e0:b1a::c0a8:b201]`
  - Non-standard port (e.g., 8080): `http://[fd7a:115c:a1e0:b1a::c0a8:b201]:8080`
- **Using MagicDNS** (if enabled):
  - HTTP: `http://192-168-178-1-via-0`
  - HTTPS: `https://192-168-178-1-via-0`
  - Non-standard port: `http://192-168-178-1-via-0:8080`

### Step 5: Test Connectivity
- **Ping Test**:
  ```
  ping fd7a:115c:a1e0:b1a::c0a8:b201
  ```
  or
  ```
  ping 192-168-178-1-via-0
  ```
- **Check Admin Console**: Verify the route appears under the subnet router.
