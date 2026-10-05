<p align="center"><img src="https://raw.githubusercontent.com/claimward/brand/main/social/claimward.png" alt="claimward" width="720"></p>

# Claimward

**Zero-Trust access to your network, on your terms.**

Claimward is a self-hosted Zero-Trust VPN built on [WireGuard](https://www.wireguard.com/),
with sign-in via **GitHub** (default), any OpenID Connect provider, or a
**go-authn** provider in front of a SAML federation. Users
authenticate with an identity provider you already have;
Claimward enrolls their device as a WireGuard peer and brings up an encrypted
tunnel to your private network — one peer per device, routes scoped to the
tenant the person chose, leases that expire on their own. Apps for macOS, Linux
and Windows.

Open source (BSD-3-Clause), written in Go: a Svelte webview UI on macOS, a
pure-Go [go-widgets](https://github.com/go-widgets) UI on Linux and Windows.

## Repositories

| Repo | What it is |
|------|-----------|
| [**claimward-vpn-server**](https://github.com/claimward/claimward-vpn-server) | Control plane: verifies GitHub, OIDC or go-authn tokens, places the device in a tenant, allocates addresses, programs the WireGuard gateway, streams route updates over gRPC |
| [**claimward-vpn-client**](https://github.com/claimward/claimward-vpn-client) | Shared Go library (wire protocol, sign-in, tunnel) and the app core + privileged helper the three apps share; it ships no binary |
| [**claimward-vpn-app-osx**](https://github.com/claimward/claimward-vpn-app-osx) | macOS app — Go tray + Svelte webview UI + privileged WireGuard helper; DMG on each release |
| [**claimward-vpn-app-linux**](https://github.com/claimward/claimward-vpn-app-linux) | Linux app — go-widgets window + tray, helper under a hardened systemd unit |
| [**claimward-vpn-app-windows**](https://github.com/claimward/claimward-vpn-app-windows) | Windows app — go-widgets window + tray, helper service, Wintun adapter |
| [**docs**](https://github.com/claimward/docs) | Documentation, versioned per release → [claimward.github.io/docs](https://claimward.github.io/docs/) |
| [**claimward.github.io**](https://github.com/claimward/claimward.github.io) | Landing page (Hugo) → [claimward.github.io](https://claimward.github.io/) |

## How it works

1. **Sign in** — the app authenticates with GitHub (device flow), an OIDC provider (browser, PKCE) or go-authn (device flow, which also registers the device's public key).
2. **Enroll** — its privileged helper sends the WireGuard public key, with that token and the chosen tenant, to a server the helper's own configuration names.
3. **Authorize** — the server verifies the token, checks the tenant, allocates an address, and adds the device as a peer.
4. **Connect** — an encrypted WireGuard tunnel comes up into your private network; the tenant's route changes are pushed to it over gRPC on TLS.

→ Read the [documentation](https://claimward.github.io/docs/) to get started.
