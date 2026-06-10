# Claimward

**Zero-Trust access to your network, on your terms.**

Claimward is a self-hosted Zero-Trust VPN built on [WireGuard](https://www.wireguard.com/)
and OpenID Connect. Users authenticate with your existing identity provider;
Claimward enrolls their device as a WireGuard peer and brings up an encrypted
tunnel to your private network — one peer per device, scoped routes, leases that
expire on their own.

Open source (BSD-3-Clause), written in Go, with a Svelte desktop UI.

## Repositories

| Repo | What it is |
|------|-----------|
| [**claimward-vpn-server**](https://github.com/claimward/claimward-vpn-server) | Control plane: verifies OIDC tokens, allocates addresses, programs the WireGuard gateway |
| [**claimward-vpn-client**](https://github.com/claimward/claimward-vpn-client) | Shared Go core (wire protocol, OIDC, tunnel) **and** the `claimward` CLI |
| [**claimward-vpn-app-osx**](https://github.com/claimward/claimward-vpn-app-osx) | macOS app — Go tray + Svelte webview UI + privileged WireGuard helper |
| claimward-vpn-app-linux · claimward-vpn-app-windows | Desktop apps (planned) |
| [**docs**](https://github.com/claimward/docs) | Documentation (MkDocs + mike) → [claimward.github.io/docs](https://claimward.github.io/docs/) |
| [**claimward.github.io**](https://github.com/claimward/claimward.github.io) | Landing page (Hugo) → [claimward.github.io](https://claimward.github.io/) |

## How it works

1. **Sign in** — the client runs an OIDC PKCE flow in the browser and gets an ID token.
2. **Enroll** — it sends its WireGuard public key to the server with that token.
3. **Authorize** — the server verifies the token, allocates an address, and adds the device as a peer.
4. **Connect** — an encrypted WireGuard tunnel comes up into your private network.

→ Read the [documentation](https://claimward.github.io/docs/) to get started.
