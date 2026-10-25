# EDP Domain Migration

## Overview

Practice programme modelling the migration of business-owned data domains to a
Databricks lakehouse (Unity Catalog, medallion architecture, declarative pipelines).

The focus is the business analysis side of a migration: eliciting requirements from
domain owners and stewards, defining data contracts, writing source-to-target
mappings and DQ expectations, and gating each domain through a readiness checklist
before it enters build.

Work is planned and tracked in Azure Boards. This repository holds the
documentation that lives alongside the code.

## Scope

| Domain | Data products | Depends on |
|---|---|---|
| Reference Data | Security Master | – |
| Fixed Income | Daily Positions, Transactions | Security Master |

## Key Stakeholders (roles)

- **Domain Owner**: accountable for business priority and definitions
- **Data Steward**: owns data quality rules and semantic definitions
- **Business Analyst / Backlog Owner**: requirements, contracts, backlog, dependencies
- **Data Engineers**: build pipelines and enforce contracts
- **Delivery Manager**: delivery plan, capacity, escalation to steering

## Success Criteria

- Every migrated data product has an agreed data contract (schema, semantics,
  DQ rules with severity, SLA, ownership, access)
- No domain enters build without passing the readiness checklist
- Gold tables reconcile to source within agreed tolerance
- Cross-domain dependencies are visible and tracked before they block delivery

## Repository Structure

| Folder | Contents |
|---|---|
| `contracts/` | Data contracts per data product (ODCS-style YAML) |
| `mappings/` | Source-to-target mappings |
| `readiness/` | Domain migration readiness checklists |
| `docs/` | Glossary, ways of working, decisions |

## Workflow Guidelines

- **Hierarchy:** Epic (domain) → Feature (data product) → User Story → Task
- **Definition of Ready:** target table and grain defined, source-to-target mapping
  linked, DQ rules with severity agreed, acceptance criteria testable
- **Definition of Done:** acceptance criteria met, DQ expectations passing,
  documentation updated, steward sign-off
- **Labels:** `type:epic`, `type:feature`, `type:story`, `domain:fixed-income`,
  `domain:reference-data`, `status:blocked`, `contract-pending`
- **Dependencies:** recorded as "Blocked by #issue" and labelled `status:blocked`

## Team Information

Maintained by Ehis Jegbefumwen ([GitHub](https://github.com/IamEhis)).
