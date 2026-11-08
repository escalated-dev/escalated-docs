# Escalated vs Intercom

Intercom provides a hosted support platform. Escalated is an MIT-licensed support package installed inside your own application, without core per-agent licence fees.

## Feature comparison

| Dimension | Escalated | Intercom |
|-----------|-----------|-----------|
| Ticket conversations | Core package | Included in the support product |
| Hosting and administration | Your host application and infrastructure | Vendor-managed service |
| Core licence fees | No per-agent licence fees | Plan and usage terms apply |

Intercom provides a shared inbox, ticketing, Messenger, and a public help center. Advanced includes workflows and round-robin assignment; Expert adds SLAs and SSO.

Plugins have separate installation and provider requirements. Channel and AI integrations are not a promise of identical behavior on every backend. Hosting, email, storage, provider usage, and maintenance still cost money with Escalated. A compliance plugin does not certify a deployment as HIPAA-compliant or SOC 2-audited.

## Key differentiators

- **Open source and self-hosted.** Escalated core is MIT-licensed and can run on your own infrastructure.
- **Embeds into your application.** Configure the backend adapter with your authentication, storage, and deployment. WordPress and Filament have native interfaces; the other supported web adapters use the shared Vue interface.
- **No core per-agent pricing.** Agent count does not change the core licence fee. Compare operating costs and the features your team actually needs.

## Migrating from Intercom

The separate MIT-licensed [`escalated-plugin-import-intercom`](https://github.com/escalated-dev/escalated-plugin-import-intercom) contains an importer. Test its mappings and API access with a small export before a full migration. See [Importing Data](/docs/importing).

## Pricing comparison

The [Intercom pricing page](https://www.intercom.com/pricing) lists the following terms. Amounts, where shown, are USD before tax.

| Plan | Published terms |
|------|-----------------|
| Essential | $29/seat/month list price; a $19 new-customer promotion is displayed |
| Advanced | $85/seat/month, billed annually |
| Expert | $132/seat/month, billed annually |

A 30-seat team on Advanced costs `30 × $85 = $2,550/month`, or `$30,600/year`, with annual billing before usage and tax.

Fin pricing starts at $0.99 per outcome. Phone, SMS, WhatsApp, and other usage can add charges; the Essential promotion has its own eligibility terms.

*Prices and requirements as of November 2026.*
