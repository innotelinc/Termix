# Termix in the Innotel Platform Stack

**Role: CodeOps** — Self-hosted, plugin-based server management.

Part of the [Innotel Platform Stack](https://github.com/innotelinc/innotel-platform-stack).
The canonical definition of the stack, its shared layers and their owners lives
there; this file records only what Termix does inside it.

## Boundaries

### Owns

- the terminal, file and tunnel surfaces
- the plugin runtime
- the deployment's host inventory

### Consumes

- SSH and SFTP on the managed hosts
- Cerulean (Authentik SSO, DNS, TLS)
- NPM Edge (public host)

### Does not own

- the hosts it manages
- identity (Authentik)
- secrets (Cerulean Vault)

## Service map

| Component | Technology | Job |
| --- | --- | --- |
| Termix | Node.js / TypeScript | Self-hosted, plugin-based server management. |
| Identity | Cerulean Authentik | Sign-in and role claims, where the repo has a UI |
| Secrets | Cerulean Vault (KV v2) | Production credentials, referenced as `vault://` |
| Trust | Cerulean | DNS, TLS and the public hostname |
| Edge | NPM Edge | The public route in front of the service |

## In the ecosystem

- **Identity** comes from Cerulean Authentik; this repo holds no second account
  table and no password of its own.
- **Secrets** come from Cerulean Vault. `.env` is local only and is never
  committed; a `vault://` reference is resolved by the deployment.
- **Trust and edge** are Cerulean's and NPM Edge's. This repo does not write DNS
  records or call the NPM API directly.
- **Storage, billing and telephony** belong to ONYX, Magnate and Zeus
  respectively; Termix consumes them only where the boundaries above say
  so.

## See also

- [README](../README.md)
- [Innotel Platform Stack](https://github.com/innotelinc/innotel-platform-stack)
