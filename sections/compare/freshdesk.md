# Escalated vs Freshdesk

Freshdesk provides a hosted support platform. Escalated is an MIT-licensed support package installed inside your own application, without core per-agent licence fees.

## Feature comparison

| Dimension | Escalated | Freshdesk |
|-----------|-----------|-----------|
| Ticket conversations | Core package | Included in the support product |
| Hosting and administration | Your host application and infrastructure | Vendor-managed service |
| Core licence fees | No per-agent licence fees | Plan and usage terms apply |

Freshdesk provides hosted ticketing, a shared inbox, and a customer portal. Its current plans include different routing, reporting, and AI allowances.

Plugins have separate installation and provider requirements. Channel and AI integrations are not a promise of identical behavior on every backend. Hosting, email, storage, provider usage, and maintenance still cost money with Escalated. A compliance plugin does not certify a deployment as HIPAA-compliant or SOC 2-audited.

## Key differentiators

- **Open source and self-hosted.** Escalated core is MIT-licensed and can run on your own infrastructure.
- **Embeds into your application.** Configure the backend adapter with your authentication, storage, and deployment. WordPress and Filament have native interfaces; the other supported web adapters use the shared Vue interface.
- **No core per-agent pricing.** Agent count does not change the core licence fee. Compare operating costs and the features your team actually needs.

## Migrating from Freshdesk

The separate MIT-licensed [`escalated-plugin-import-freshdesk`](https://github.com/escalated-dev/escalated-plugin-import-freshdesk) contains an importer. Test its mappings and API access with a small export before a full migration. See [Importing Data](/docs/importing).

## Pricing comparison

The [Freshdesk pricing page](https://www.freshworks.com/freshdesk/pricing/) lists the following terms. Amounts, where shown, are USD before tax.

| Plan | Published terms |
|------|-----------------|
| Growth | $19/agent/month, billed annually |
| Pro | $55/agent/month, billed annually |
| Enterprise | $89/agent/month, billed annually |

A 25-agent team on Pro costs `25 × $55 = $1,375/month`, or `$16,500/year`, with annual billing before add-ons and tax.

Freshdesk has a [Free Program](https://support.freshdesk.com/support/solutions/articles/50000010099-explore-freshdesk-free-program-freshdesk-only-) for two agents for six months. It is not an unlimited ten-agent free tier.

*Prices and requirements as of November 2026.*
