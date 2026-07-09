# VibeNest Template: Vaultwarden

This is a security-review adapter draft for [Vaultwarden](https://github.com/dani-garcia/vaultwarden).

It does not fork or modify Vaultwarden. This repo is intentionally not marked Ready in VibeNest until the security checklist is complete:

- generated admin token strategy
- registration policy
- TLS and domain guidance
- backup guidance for `/data`
- clear warnings for password-manager ownership

## VibeNest notes

Do not enable one-click deploy from the public catalog until smoke and security review pass. The compose file is a starting point for review, not a production promise.

## Upstream

- Product: https://github.com/dani-garcia/vaultwarden
- Docker image: `vaultwarden/server:latest`
