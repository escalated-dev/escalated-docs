# Escalated vs Help Scout

Help Scout provides a hosted support platform. Escalated is an MIT-licensed support package installed inside your own application, without core per-agent licence fees.

## Feature comparison

| Dimension | Escalated | Help Scout |
|-----------|-----------|-----------|
| Ticket conversations | Core package | Included in the support product |
| Hosting and administration | Your host application and infrastructure | Vendor-managed service |
| Core licence fees | No per-agent licence fees | Plan and usage terms apply |

Help Scout provides inboxes, saved replies, and knowledge bases. Standard includes a basic SLA policy; Plus adds a customer portal and round-robin routing. Pro includes SSO/SAML.

Plugins have separate installation and provider requirements. Channel and AI integrations are not a promise of identical behavior on every backend. Hosting, email, storage, provider usage, and maintenance still cost money with Escalated. A compliance plugin does not certify a deployment as HIPAA-compliant or SOC 2-audited.

## Key differentiators

- **Open source and self-hosted.** Escalated core is MIT-licensed and can run on your own infrastructure.
- **Embeds into your application.** Configure the backend adapter with your authentication, storage, and deployment. WordPress and Filament have native interfaces; the other supported web adapters use the shared Vue interface.
- **No core per-agent pricing.** Agent count does not change the core licence fee. Compare operating costs and the features your team actually needs.

## Migrating from Help Scout

The separate MIT-licensed [`escalated-plugin-import-helpscout`](https://github.com/escalated-dev/escalated-plugin-import-helpscout) contains an importer. Test its mappings and API access with a small export before a full migration. See [Importing Data](/docs/importing).

## Pricing comparison

The [Help Scout pricing page](https://www.helpscout.com/pricing/) lists the following terms. Amounts, where shown, are USD before tax.

| Plan | Published terms |
|------|-----------------|
| Standard | $25/user/month at the displayed per-user rate |
| Plus | $45/user/month at the displayed per-user rate |
| Pro | $75/user/month at the displayed per-user rate |

A 20-user team on Standard costs `20 × $25 = $500/month`, or `$6,000/year`, at that displayed rate before add-ons and tax.

The Free plan lists five users, one inbox, and one Docs site. AI resolution charges are separate from user pricing.

*Prices and requirements as of November 2026.*
