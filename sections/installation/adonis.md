## 1. Install the package

```bash
git clone https://github.com/escalated-dev/escalated-adonis.git
cd escalated-adonis
npm ci
npm run build
```

The source package is not published on npm. Install the built local package into your host app and satisfy the peer dependencies in its `package.json` before running the host-side steps below.

## 2. Configure the package

```bash
node ace configure @escalated-dev/escalated-adonis
```

## 3. Run migrations

```bash
node ace migration:run
```

> **Note:** The configure command publishes `config/escalated.ts`, registers the provider, and copies migrations automatically.
