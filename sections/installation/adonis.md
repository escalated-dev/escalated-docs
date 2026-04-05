## 1. Install the package

```bash
$ npm install @escalated-dev/escalated-adonis
```

## 2. Configure the package

```bash
$ node ace configure @escalated-dev/escalated-adonis
```

## 3. Run migrations

```bash
$ node ace migration:run
```

> **Note:** The configure command publishes `config/escalated.ts`, registers the provider, and copies migrations automatically.

## Headless mode (optional)

To run Escalated without the built-in Inertia UI, set this in your `.env`:

```
ESCALATED_UI_ENABLED=false
```

API routes, management commands, events, and the plugin runtime continue to work normally.
