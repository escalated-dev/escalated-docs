# Single Sign-On (SSO)

Escalated supports SAML 2.0 and JWT-based single sign-on. When enabled, users authenticate through your identity provider instead of the built-in login form.

## Configuration

SSO is configured through the admin panel under **Settings → SSO**, or programmatically via the `EscalatedSettings` model.

### SSO Provider

Set `sso_provider` to one of:

| Provider | Value | Description |
|----------|-------|-------------|
| Disabled | `none` | SSO is off (default) |
| SAML 2.0 | `saml` | SAML assertion-based SSO |
| JWT | `jwt` | JSON Web Token-based SSO |

## SAML Configuration

When `sso_provider` is `saml`, configure:

| Setting | Description |
|---------|-------------|
| `sso_entity_id` | Your Identity Provider's Entity ID (issuer). Must match the `<Issuer>` in SAML assertions. |
| `sso_url` | Your IdP's SSO login URL |
| `sso_certificate` | Your IdP's X.509 signing certificate (PEM format, without header/footer is fine) |

### How it works

1. User visits Escalated login
2. Escalated redirects to your IdP's SSO URL
3. User authenticates with the IdP
4. IdP posts a base64-encoded SAML response back to Escalated
5. Escalated validates the assertion: signature, issuer, timestamps, and extracts user attributes

### Validation checks

- **Signature** — verified against the configured certificate (SHA-256, with SHA-1 fallback)
- **Issuer** — must match `sso_entity_id`
- **Conditions** — `NotBefore` and `NotOnOrAfter` are checked with 2-minute clock skew tolerance
- **Attributes** — extracted from `<AttributeStatement>`, with NameID as email fallback

## JWT Configuration

When `sso_provider` is `jwt`, configure:

| Setting | Description |
|---------|-------------|
| `sso_jwt_secret` | Shared secret (for HMAC) or public key (for RSA) |
| `sso_jwt_algorithm` | Signing algorithm (default: `HS256`) |

### Supported algorithms

| Algorithm | Type | Description |
|-----------|------|-------------|
| `HS256` | HMAC | HMAC-SHA256 with shared secret |
| `HS384` | HMAC | HMAC-SHA384 with shared secret |
| `HS512` | HMAC | HMAC-SHA512 with shared secret |
| `RS256` | RSA | RSA-SHA256 with public key |
| `RS384` | RSA | RSA-SHA384 with public key |
| `RS512` | RSA | RSA-SHA512 with public key |

### How it works

1. Your application generates a signed JWT containing the user's email
2. Redirect the user to Escalated's SSO endpoint with the token
3. Escalated verifies the signature, checks expiration, and extracts user attributes

### Required JWT claims

| Claim | Description |
|-------|-------------|
| `email` (or mapped attribute) | User's email address (required) |
| `exp` | Expiration timestamp (recommended) |
| `nbf` | Not-before timestamp (optional) |

## Attribute Mapping

Both SAML and JWT support custom attribute mapping:

| Setting | Default | Description |
|---------|---------|-------------|
| `sso_attr_email` | `email` | Attribute/claim containing the user's email |
| `sso_attr_name` | `name` | Attribute/claim containing the user's display name |
| `sso_attr_role` | `role` | Attribute/claim containing the user's role |

## Framework Support

SSO is available across all backends:

| Framework | Service | Location |
|-----------|---------|----------|
| Laravel | `SsoService` | `src/Services/SsoService.php` |
| Django | `SsoService` | `escalated/services/sso_service.py` |
| Rails | `SsoService` | `lib/escalated/services/sso_service.rb` |
| AdonisJS | `SsoService` | `src/services/sso_service.ts` |
| WordPress | `SsoService` | `includes/Services/SsoService.php` |
| Filament | Admin Page | **Settings → SSO** in the Filament panel |
