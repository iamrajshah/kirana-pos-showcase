# Kirana SaaS architecture

Kirana has three deployable applications and one shared database. The POS and
Platform Admin are separate frontends; both use the same modular Express API.
There is no direct browser-to-database access and no separate admin or billing
microservice.

```mermaid
flowchart LR
  subgraph people[People]
    staff[Shop owner / manager / cashier]
    operator[Rajesh / platform operator]
  end

  subgraph clients[Client applications]
    pos[Kirana POS<br/>kirana-ui<br/>Web + Capacitor mobile]
    admin[Kirana Platform Admin<br/>kirana-admin<br/>Private internal web app]
  end

  subgraph api[One Railway application service]
    server[kirana-server<br/>Express / TypeScript / Prisma]
    tenantAuth[POS identity + tenant JWT]
    adminAuth[Admin cookie session + CSRF + scopes]
    commercial[Plans + subscriptions + feature gates]
    domain[Billing + stock + khata + purchases + reports]
    operations[Onboarding + shops + renewals + audit]
  end

  subgraph data[Railway data layer]
    mysql[(MySQL)]
    tenantData[Tenant business tables<br/>isolated by tenant_id]
    platformData[Control-plane tables<br/>admins, plans, subscriptions,<br/>renewals and audit]
  end

  staff --> pos
  operator --> admin
  pos -->|HTTPS /api/v1<br/>Bearer JWT| server
  admin -->|same-origin /api proxy<br/>Secure cookie + CSRF| server
  server --> tenantAuth
  server --> adminAuth
  tenantAuth --> commercial
  tenantAuth --> domain
  adminAuth --> operations
  commercial --> mysql
  domain --> mysql
  operations --> mysql
  mysql --> tenantData
  mysql --> platformData
```

## Deployment view

| Application | Current target | Important rule |
| --- | --- | --- |
| `kirana-ui` | Netlify web; Capacitor mobile packages | Calls the API through `/api/v1`; automatic Netlify production builds remain disabled |
| `kirana-admin` | Netlify when credits are available | Private repository; `/api/*` is proxied through the admin origin so the strict session cookie works |
| `kirana-server` | Railway | The only backend; owns authorization, commercial enforcement, transactions and audit |
| MySQL | Railway | Shared schema; tenant business rows carry `tenant_id`, while control-plane records use dedicated tables |

The private admin repository protects source visibility, not the deployed URL.
The application login, scoped server session, CSRF protection and origin allowlist
are the access boundary. Platform Admin can operate SaaS lifecycle metadata but
cannot use its identity to browse a shop's transactional records.

## Typical flows

1. A shop user signs in to the POS. The API resolves identity, tenant,
   subscription and role before returning tenant-scoped data.
2. Billing, khata, purchase and reporting requests stay inside the same API and
   are filtered by `tenant_id` before Prisma reaches MySQL.
3. A platform operator signs in to the standalone admin app. Netlify proxies the
   request to Railway on the same browser origin, preserving the secure cookie.
4. Admin actions pass origin, session, scope and CSRF checks. Sensitive actions
   additionally require fresh password confirmation and an operator reason.
5. Onboarding, plan, subscription and renewal decisions are audit logged. The
   POS sees only the resulting commercial access and shop-facing recovery state.

