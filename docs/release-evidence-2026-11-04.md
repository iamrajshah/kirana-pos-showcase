# Release evidence — 4 November 2026

This public summary intentionally excludes credentials, private infrastructure,
customer data, raw database details, and operating secrets.

## Scope

- Staff POS on desktop, tablet, mobile web, and Android debug packaging
- Private Platform Admin control plane
- Tenant-branded customer Bazaar
- Shared tenant-isolated API and relational data model
- Expiry-aware receiving/stock, purchase-bill review/import, and GST/CA reports

## Results

| Verification | Result |
| --- | --- |
| Read-only production API journey | 44/44 passed |
| New expiry/import/GST production API journey | 24/24 passed |
| Responsive browser matrix | 62/62 passed |
| Server automated suite | 154 suites / 966 tests passed |
| Customer storefront suite | 10 release checks + 36 tests passed |
| Android debug verification | Unit checks, lint, and 399 Gradle tasks passed |

The responsive matrix covered Platform Admin desktop; POS desktop, tablet and
mobile; and Customer Bazaar desktop, tablet and mobile. It checked authentication,
protected routes, core business pages, tenant identity, offers, product detail,
expiry alerts, purchase import and GST/CA workspaces with no remaining runtime or
console error.

## Safety boundaries

- Tenant identity is server-derived and enforced for protected business data.
- Purchase extraction creates a review draft; no stock or ledger changes before
  explicit confirmation.
- Expired units remain physically traceable but are excluded from saleable stock.
- GST outputs prepare records for a qualified accountant; the product does not
  claim GST filing, e-invoice/IRN, or e-way-bill submission.
- Plan packaging, global feature state, subscription state, and role policy are
  independently enforced by the API.

## Remaining publication work

The web release is qualified for demonstration. Play Store publication still
requires a production-signed Android App Bundle, final listing assets/versioning,
and a physical-device pass for camera, barcode, printer, and native file sharing.
Tax exports require representative review by a qualified CA before a compliance
claim.
