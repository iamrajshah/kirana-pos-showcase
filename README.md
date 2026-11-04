# Kirana POS

> A mobile-first retail operating system that helps neighbourhood stores bill faster and act on dues, low stock, and held transactions without digging through reports.

<p align="center">
  <img src="assets/hero.png" alt="Kirana POS running on desktop and mobile" width="100%" />
</p>

<p align="center">
  <img alt="React" src="https://img.shields.io/badge/React-18-149eca?style=flat-square&logo=react&logoColor=white" />
  <img alt="Ionic" src="https://img.shields.io/badge/Ionic-7-3880ff?style=flat-square&logo=ionic&logoColor=white" />
  <img alt="TypeScript" src="https://img.shields.io/badge/TypeScript-5-3178c6?style=flat-square&logo=typescript&logoColor=white" />
  <img alt="Node.js" src="https://img.shields.io/badge/Node.js-API-339933?style=flat-square&logo=nodedotjs&logoColor=white" />
  <img alt="MySQL" src="https://img.shields.io/badge/MySQL-Data-4479a1?style=flat-square&logo=mysql&logoColor=white" />
  <img alt="AI-assisted engineering" src="https://img.shields.io/badge/Engineering-AI--assisted-7c3aed?style=flat-square" />
</p>

## The product

Kirana POS brings the daily operating work of a small retailer into one responsive product: walk-in billing, barcode-assisted product lookup, stock visibility, customer credit, supplier purchasing, payments, and business reporting.

The experience is designed around the counter rather than around accounting terminology. An owner sees what needs attention, a cashier can create a bill without unnecessary customer setup, and the same workflows adapt from a desktop screen to a phone.

## Watch the product

[Watch the complete 8 minute 30 second Kirana POS walkthrough](demo/kirana-pos-client-demo.mp4)

The narrated walkthrough shows the private Platform Admin briefly, then follows
real shop workflows: a fast cash sale with private estimated profit, an unpaid
bill, customer sorting and collection, invoices, stock/barcodes, purchases,
supplier khata, reports, firms, staff, language/theme, and a customer Bazaar
order through fulfilment and payment. It includes desktop, tablet and mobile
views, English captions and chapter markers. The 720p download is about 26 MB.

[Watch the shorter 38-second product tour](demo/kirana-pos-demo.mp4)

The recording uses a deployed demo tenant with synthetic products, customers, balances, and transactions. It contains no real customer data or access credentials.

See [the walkthrough chapter guide](demo/CLIENT_WALKTHROUGH.md) for timestamps
and the suggested order for a live sales demonstration.

## Product walkthrough

### Decisions first

The owner dashboard turns operational signals into direct actions: collect an outstanding balance, replenish a low-stock item, or resume a held bill.

<p align="center">
  <img src="assets/owner-dashboard-desktop.png" alt="Kirana POS owner dashboard showing money to collect, low stock and held bills" width="100%" />
</p>

### Fast walk-in billing

A cashier can search or scan a product, add it to a walk-in bill, adjust quantity or price, and collect through cash, UPI, card, or another payment method. Customer creation is optional for immediate-payment sales.

<table>
  <tr>
    <td width="50%"><img src="assets/fast-billing-search.png" alt="Product search in the Kirana POS billing workflow" /></td>
    <td width="50%"><img src="assets/fast-billing-cart.png" alt="Walk-in bill with a product and payment choices" /></td>
  </tr>
  <tr>
    <td align="center"><strong>Search or scan</strong></td>
    <td align="center"><strong>Collect or hold</strong></td>
  </tr>
</table>

### A catalogue built for store operations

Products are grouped for fast discovery and can carry SKUs, prices, active status, stock rules, variants, and reusable barcode labels for store-packed or loose items.

<p align="center">
  <img src="assets/product-catalogue.png" alt="Kirana POS product catalogue grouped by category" width="100%" />
</p>

### A tenant-branded online Bazaar

Every participating shop can share its own tenant-safe link. Customers browse a
responsive marketplace, discover published offers, add products, verify their
phone at checkout, and follow order status while the shop fulfils the request in
the POS.

<table>
  <tr>
    <td width="72%"><img src="assets/customer-bazaar-desktop.png" alt="Tenant-branded customer Bazaar on desktop" /></td>
    <td width="28%"><img src="assets/customer-bazaar-mobile.png" alt="Customer Bazaar on a mobile phone" /></td>
  </tr>
</table>

### Expiry-aware purchasing and CA preparation

Received stock can carry batch and expiry facts so billing works from saleable
stock and owners can act before products become a loss. Supplier bills can be
read from a PDF or photo into an editable review instead of writing directly to
stock. Firm-scoped GST summaries, registers, HSN/UQC analysis, and CSV exports
prepare records for a CA without pretending to file a return.

<table>
  <tr>
    <td width="50%"><img src="assets/purchase-bill-import.png" alt="Review-first supplier bill import" /></td>
    <td width="50%"><img src="assets/gst-ca-reports.png" alt="GST and CA preparation workspace" /></td>
  </tr>
</table>

### Each shop gets its own feature choices

Platform Admin can keep a feature on its plan default, enable it for a shop, or
disable it for that shop. Optional expiry dates support a limited pilot; every
change requires a reason and leaves an audit record. Existing POS sessions
refresh their access automatically, while the API enforces the current policy.

The shop setting works alongside subscription status, feature prerequisites and
staff permissions. It does not change another shop's settings or remove its
existing bills, stock and account history.

<p align="center">
  <img src="assets/shop-feature-access.png" alt="Platform Admin feature access for one synthetic demonstration shop, showing plan inheritance, availability and staff roles" width="100%" />
</p>

### Mobile where it matters

The mobile layout keeps the important actions within reach and preserves the same decision-oriented dashboard instead of reducing the phone experience to a read-only companion.

<p align="center">
  <img src="assets/owner-dashboard-mobile.png" alt="Kirana POS owner dashboard on a mobile phone" width="340" />
</p>

## What I built

- A responsive Ionic React client for owner, manager, and cashier workflows.
- Fast billing with walk-in sales, product search, barcode scanning, held bills, editable quantities and multiple payment modes.
- Inventory, catalogue, customer ledger, supplier, purchase, payment, and reporting workflows.
- Batch-aware expiry alerts, saleable-stock protection, FEFO allocation, and controlled write-off.
- Review-first supplier bill import from text PDF or image OCR.
- Firm-scoped GST and CA preparation reports with HSN/UQC and CSV export.
- Tenant-branded customer Bazaar with offers, OTP checkout, and live order status.
- Tenant-aware product and operational data boundaries for a shared SaaS platform.
- Audited feature controls for each shop, with plan inheritance, optional expiry and runtime access refresh.
- Redux Toolkit and RTK Query state management with authenticated API access and cache invalidation.
- JWT access and refresh handling, protected routes, role-aware navigation, and idempotency on sensitive billing operations.
- Mobile packaging through Capacitor, with layouts tested from narrow phone widths to desktop screens.
- Automated tests, linting, production builds, and CI/CD-oriented delivery practices.

The 4 November 2026 qualification includes 126 deployed route/API checks,
113 role checks, seven real billing-to-customer-order browser scenes, and
dedicated stock/accounting, shop-access, dark-dialog and PDF checks.
The final purchase layout also passed 20 rendered mobile/tablet checks and
focused, scrolled Android emulator checks in both themes. These supplement the
functional device checks; physical barcode, printer and sharing checks remain.
See [the public release evidence](docs/release-evidence-2026-11-04.md) for the
individual results and device-specific limits.

## Product decisions that mattered

| Challenge | Decision |
| --- | --- |
| Counter speed | Allow immediate walk-in billing without forcing customer creation |
| Owner attention | Put receivables, low stock, and held bills on the landing dashboard with direct actions |
| Mixed catalogue | Support search, scanning, SKUs, categories, pack sizes, and reusable barcode labels |
| Shared SaaS platform | Keep tenant identity and authorization in every protected business operation |
| Duplicate submissions | Use idempotency keys around billing operations that must not be repeated |
| Different devices | Design the same workflow for desktop, tablet, and phone instead of building a separate reduced mobile product |
| Operational safety | Keep the production API, credentials, deployment configuration, and real data outside this public showcase |

## Architecture

<p align="center">
  <img src="assets/architecture.svg" alt="Kirana POS architecture showing the store team, Ionic React client, private API and data services" width="100%" />
</p>

The public diagram shows product boundaries without exposing live infrastructure, private endpoints, credentials, operational procedures, or customer information. The application is a modular client and API platform—not a collection of artificial microservices.

## AI-assisted engineering

Kirana POS is developed with AI-assisted engineering across product exploration, implementation, test design, review, documentation, and demo preparation. AI accelerates the feedback loop; architecture decisions, security boundaries, verification, and release responsibility remain human-owned.

The practical goal is not to generate the most code. It is to move from an idea to a reviewable, tested product increment with less avoidable rework.

## Public and private boundaries

- The [Kirana POS client repository](https://github.com/iamrajshah/kirana-ui) is available for technical evaluation.
- The production API, infrastructure configuration, deployment controls, and operational data remain private.
- The hosted demo uses a seeded tenant. Access may be shared privately with recruiters or collaborators.
- This showcase contains no passwords, reusable tokens, private URLs, or customer data.

## About the builder

Built independently by [Rajesh Shah](https://github.com/iamrajshah), a lead full-stack engineer focused on product-minded architecture, TypeScript platforms, mobile delivery, and AI-assisted engineering.

Connect on [LinkedIn](https://www.linkedin.com/in/iamrajshah/).

---

This repository is a public product showcase. Product assets and source code are not licensed for reuse or redistribution.
