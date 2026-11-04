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
| Server automated suite | 160 suites / 1,019 tests passed |
| POS automated suite | 115 files / 555 tests passed; combined dev CI green |
| Platform Admin automated suite | 86 tests passed |
| Customer storefront | 16 release checks, 41 unit tests and 9 built-browser scenarios passed |
| Actual manager/cashier permissions and navigation | 113/113 passed |
| Per-shop feature controls | Storefront 13/13 and Reports 15/15 passed; original settings restored |
| Deployed light/dark dialogs | 68/68 passed on desktop and mobile |
| Stock, purchasing, supplier, shift, expiry, import and restore | 43/43 deployed API checks passed; original demo data restored |
| Nonzero sales/HSN export reconciliation | 10/10 passed |
| Production receipt output | 20/20 at 80 mm and 20/20 at 58 mm; normal download remains A4 |
| Deployed responsive routes and API reads | 126/126 passed across Admin, POS and customer storefront |
| Guest product detail, cart and shop isolation | 21/21 passed at phone, tablet and desktop widths |
| Cash, khata, collections, offers and customer order fulfilment | 7/7 real browser scenes passed; original demo data restored |
| Repeated held-bill resume | 21/21 passed on the deployed release; original demo data restored |
| Authorized purchase-cost prefill | 7/7 read-only deployed browser checks passed |
| Android debug build | Unit checks, lint, and 399 Gradle tasks passed |
| Installed Android emulator | Login/device cap, secure token storage, navigation, dark payment dialog/Back, private cost prefill and injected-failure recovery passed |

These are separate, overlapping test groups rather than a combined count of
unique business scenarios. The role checks use actual authenticated manager and
cashier accounts. Browser coverage checks real rendered controls and console
errors, including typing and delivery submission at 390, 820 and 1440 pixels.

Per-shop checks verified that disabling a feature affects only the selected
shop, that its API denies access, and that an already-open POS session refreshes
its navigation without a deployment. Negative tests cover stale edits, missing
CSRF, authentication, role/dependency restrictions and override expiry.

Receipt verification inspects the generated PDF rather than only a mocked print
callback: 58/80 mm dimensions, readable nonblank content, MRP savings and absence
of private profit. The Customer build now verifies the installed Ionic runtime
and exercises input changes in the built browser artifact.

The live business journey also verifies sidebar Dashboard navigation directly
after collecting payment, without refreshing the page. The held-bill drill
claims, releases and reclaims the same bill in one retained screen. Purchase
prefill uses the protected cost endpoint and preserves typed prices, repeated
selection and pack conversion.

## Safety boundaries

- Tenant identity is server-derived and enforced for protected business data.
- Purchase extraction creates a review draft; no stock or ledger changes before
  explicit confirmation.
- Expired units remain physically traceable but are excluded from saleable stock.
- GST outputs prepare records for a qualified accountant; the product does not
  claim GST filing, e-invoice/IRN, or e-way-bill submission.
- Plan packaging, global feature state, subscription state, and role policy are
  independently enforced by the API.
- Shop-specific overrides have an audit record, optional expiry and a restore
  path. Core account recovery remains protected.
- Shared billing catalogue/search responses contain no purchase costs;
  confidential cost access and private profit follow their authorized paths.

## Remaining publication work

The web release is qualified for demonstration. Play Store publication still
requires a production-signed Android App Bundle, final listing assets/versioning,
and a physical-device pass for camera, barcode, printer, and native file sharing.
Tax exports require representative review by a qualified CA before a compliance
claim.
