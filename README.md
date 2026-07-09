# VibeNest Template: Vaultwarden

This is a VibeNest security-review adapter draft for [Vaultwarden](https://github.com/dani-garcia/vaultwarden).

It does not fork or modify Vaultwarden. The wrapper only supplies VibeNest-safe deploy defaults:

- official `vaultwarden/server:latest` image;
- public compose service named `app` on port `80` for Coolify domain binding;
- `APP_URL` mapped to Vaultwarden `DOMAIN` so the app sees its HTTPS VibeNest subdomain;
- public self-registration disabled by default;
- invitations left enabled so the owner can create the first user from `/admin`;
- generated `ADMIN_PASSWORD` passed as Vaultwarden `ADMIN_TOKEN`;
- explicit `SIGNUPS_ALLOWED=false`, `INVITATIONS_ALLOWED=true`, `WEBSOCKET_ENABLED=true`
  and `LOG_LEVEL=warn` defaults in `.env.example` so platform env sync can show and
  preserve the security posture;
- persistent `/data` volume.

## VibeNest notes

Do not enable one-click deploy from the public catalog until smoke and security review pass.

Smoke must verify:

- the public URL opens the real Vaultwarden web vault;
- `/admin` opens and is protected by the generated admin token;
- anonymous/uninvited registration is blocked;
- `/data` is persistent;
- copy warns users to configure backups before storing real passwords.

Current smoke notes:

- VibeNest deploy reached `running`, Coolify reported `running:healthy` with
  `restart_count=0`, and the public URL opened `<title page-title>Vaultwarden Web</title>`.
- `/admin` returned `Vaultwarden Admin Panel` and the admin-token form.
- An anonymous `/identity/accounts/register` request returned
  `Registration not allowed or user already exists`.

Security release notes:

- VibeNest provides HTTPS/free SSL at the public subdomain.
- The generated `ADMIN_PASSWORD` is a high-entropy bootstrap token. Upstream recommends replacing the admin token with an Argon2 PHC hash for long-term production use.
- Users should invite/create their first account from `/admin`, then keep public signups disabled.
- Treat backups as mandatory: the SQLite database, attachments, sends, config and RSA keys live under `/data`.

## Upstream

- Product: https://github.com/dani-garcia/vaultwarden
- Docker image: `vaultwarden/server:latest`
