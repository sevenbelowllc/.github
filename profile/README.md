<div align="center">

# SevenBelow

**Compliance OS — multi-tenant compliance management for modern teams.**

[sevenbelow.com](https://www.sevenbelow.com) · [LinkedIn](https://www.linkedin.com/company/sevenbelow)

</div>

---

## What we build

**Compliance OS** is a SOC 2 + GDPR + NIST CSF 2.0 platform that pairs strict tenant isolation with an AI agent runtime — so onboarding, policy authoring, evidence collection, and control mapping stop being spreadsheets and start being software.

| Module | Stack | Purpose |
|--------|-------|---------|
| **compliance-ui** | Next.js 16 · React 18 · Apollo Client · Clerk | Operator + auditor frontend, AI onboarding wizard, reviewer inbox |
| **compliance-core** | Express 5 · Apollo Server 5 · PostgreSQL 18 · pgvector | GraphQL + REST API, RLS-enforced tenant boundaries, evidence + cost ledger |
| **agent-core** | Python 3.12 · LangGraph · MCP · asyncpg | Tenant-bound agent runtime, MCP tool surface, HITL approval gate |

---

## How we run

- **Tenant isolation contract** — every Class T table composite-keyed on `tenant_id`, Postgres RLS forced fail-closed, runtime role NOBYPASSRLS. Cross-tenant access is impossible at the database layer.
- **AI safety by construction** — every AI-authored row carries an `ai_lineage` JSONB breadcrumb (model, prompt hash, run id, tool call id). Every write is gated by a Reviewer Inbox for human Confirm / Reject. Air-gap risk ladder per tool call.
- **7-year immutable cost ledger** — every LLM call is priced and written to `tenant_cost_events` with a GENERATED STORED retention column. Auditable from day one.
- **Defense in depth** — Cloudflare WAF → GCP Cloud Armor (OWASP CRS v3.3) → GKE NetworkPolicy default-deny → Clerk JWT → Postgres RLS → immutable audit.

---

## Status

Compliance OS is in active development on `nonprod` (`https://integration.sevenbelow.com`). Public repos surface platform components and tooling; production rollout follows the standard SOC 2 readiness path.

For partnership, evaluation, or hiring: **<dev@sevenbelow.com>**.

---

<div align="center">
<sub>© SevenBelow LLC · Built with discipline · Audited by design</sub>
</div>
