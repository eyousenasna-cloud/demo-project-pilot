# PRD: 6-Month AI-Assisted Engineering Pilot

| Field | Value |
| --- | --- |
| Status | Draft |
| Owner | Eddie (Software Engineer) – Pilot Lead |
| Executive Sponsor | _TBD (VP/Director of Engineering)_ |
| Pilot Duration | 6 months (26 weeks) |
| Last Updated | 2026-11-23 |
| Companion Doc | [PLAN.md](./PLAN.md) |

---

## 1. Summary

We will run a 6-month, time-boxed pilot to evaluate AI tooling across the software development lifecycle: AI coding assistants in the IDE, autonomous or background coding agents, AI-assisted code review, and AI support for tests and documentation. The pilot is meant to produce **evidence**, not opinions. At the end we decide whether to **scale, adjust, or stop**, based on pre-agreed success metrics covering productivity, quality, security, cost, and developer experience.

## 2. Problem Statement

- Engineering throughput is limited by repetitive work: boilerplate, tests, migrations, bug triage, documentation, and code review wait times.
- Engineers are already trying AI tools on their own, without consistent guardrails, data-handling rules, or ways to measure impact.
- Leadership has no reliable data on whether AI tools deliver real ROI or what risks they add (security, IP, quality, over-reliance).

## 3. Goals

1. **Measure impact** of AI tooling on delivery speed and code quality, compared against a baseline.
2. **Find the high-value use cases** (and the low-value ones) for our codebase and workflows.
3. **Set guardrails** for security, privacy, IP, and compliance that could scale org-wide.
4. **Measure developer experience** and adoption over time.
5. **Make a data-driven go/no-go recommendation**, with a cost model, for an org-wide rollout.

## 4. Non-Goals

- Replacing engineers or reducing headcount. The pilot is about augmenting engineers.
- Building custom foundation models or fine-tuning in-house models.
- Rolling out to the whole organization during the pilot.
- Using AI on regulated or customer PII data without explicit Security/Legal approval.
- Picking a permanent vendor. The pilot informs that decision but doesn't make it.

## 5. Target Users & Personas

| Persona | Description | Primary Use Cases |
| --- | --- | --- |
| Product Engineer | Builds features in app/service code | Code generation, refactors, unit tests |
| Platform/Infra Engineer | Owns CI/CD, infra-as-code, tooling | Scripts, IaC, migrations, debugging |
| QA / SDET | Owns test strategy and automation | Test generation, flaky-test triage |
| Tech Lead / Reviewer | Reviews PRs, mentors | AI-assisted code review, design summaries |
| Engineering Manager | Owns team delivery | Adoption and impact dashboards |
| New Hire | Onboarding to the codebase | Codebase Q&A, explanations |

## 6. Scope

### In Scope (use cases)

| # | Use Case | Description | Priority |
| --- | --- | --- | --- |
| UC1 | IDE coding assistant | Autocomplete, inline edits, chat with codebase context | P0 |
| UC2 | Unit/integration test generation | Generate and maintain tests for new and legacy code | P0 |
| UC3 | AI-assisted code review | Automated PR review comments and bug detection | P0 |
| UC4 | Background coding agents | Agents complete scoped tickets (bugs, small features, chores) and open PRs | P1 |
| UC5 | Codebase Q&A / onboarding | Natural-language questions about architecture and code | P1 |
| UC6 | Documentation generation | READMEs, API docs, ADR drafts, changelogs | P2 |
| UC7 | Migrations & tech-debt chores | Dependency upgrades, API migrations, lint fixes | P2 |

### Out of Scope

- Production incident auto-remediation without a human in the loop.
- AI-generated code merged without human review.
- Repositories marked restricted (see Section 10).

## 7. Requirements

### 7.1 Functional Requirements

| ID | Requirement | Priority |
| --- | --- | --- |
| FR1 | Pilot participants get access to the selected AI tools via SSO | P0 |
| FR2 | Tools work with our primary languages, IDEs, and source control | P0 |
| FR3 | AI-generated PRs and review comments are identifiable (labels/tags) for measurement | P0 |
| FR4 | All AI-authored code goes through the standard human code review and CI gates | P0 |
| FR5 | Usage telemetry (seats active, suggestions accepted, agent runs, PRs) is exportable | P0 |
| FR6 | Admins can restrict tools to approved repositories | P0 |
| FR7 | Background agents can be triggered from the issue tracker or chat for scoped tasks | P1 |
| FR8 | A shared prompt and rules library exists for team conventions | P1 |

### 7.2 Non-Functional Requirements

| ID | Requirement |
| --- | --- |
| NFR1 | **Security:** vendor has SOC 2 Type II (or equivalent); data encrypted in transit and at rest |
| NFR2 | **Privacy:** zero data retention / no training on our code, contractually guaranteed |
| NFR3 | **Access control:** SSO/SAML, SCIM provisioning, role-based admin |
| NFR4 | **Auditability:** audit logs of usage and admin actions are retained for the length of the pilot |
| NFR5 | **Secrets:** no secrets in prompts; secret scanning on all AI-generated PRs |
| NFR6 | **Licensing/IP:** code-similarity / license filtering enabled where available |
| NFR7 | **Availability:** if a tool goes down, normal development continues unaffected |

## 8. Success Metrics

Metrics are measured against a **baseline** taken in Month 1 (the previous 3 months of historical data plus a pre-pilot survey). Where possible we compare pilot teams against a **comparison group** of non-pilot teams with similar work.

### 8.1 North Star

> **Increase in throughput of production-quality work per engineer, with no drop in quality or security.**

### 8.2 Primary Metrics (decide go/no-go)

| Category | Metric | Baseline Source | Target (by Month 6) |
| --- | --- | --- | --- |
| Productivity | PR cycle time (open to merge), median | Git/SCM analytics | **20% reduction** |
| Productivity | Merged PRs per engineer per week | Git/SCM analytics | **15% increase** |
| Productivity | Lead time for changes (commit to production) – DORA | CI/CD | **15% reduction** |
| Quality | Change failure rate – DORA | Incident/deploy logs | **No increase** (within ±2 pts) |
| Quality | Escaped defects per release (bugs found post-merge) | Issue tracker | **No increase** |
| Security | High/critical findings in AI-assisted code vs. non-AI code | SAST / security scans | **Not higher than baseline** |
| Adoption | Weekly active users / licensed seats | Vendor telemetry | **≥ 70%** |
| Developer Experience | Satisfaction with AI tools (1–5) | Pulse survey | **≥ 4.0** |

### 8.3 Secondary Metrics (inform rollout design)

| Category | Metric | Target |
| --- | --- | --- |
| Productivity | Self-reported hours saved per engineer per week | ≥ 3 hrs |
| Productivity | Suggestion / edit acceptance rate | ≥ 25% (tracked, not gated) |
| Agents | Agent-opened PRs merged with minimal rework | ≥ 50% merge rate |
| Agents | Share of eligible chore/bug tickets completed by agents | ≥ 20% |
| Quality | Test coverage on pilot repos | +10 percentage points |
| Quality | Code review turnaround (time to first review) | 25% reduction |
| Onboarding | Time to first merged PR for new hires | 30% reduction |
| DevEx | Net Promoter Score for AI tools | ≥ +30 |
| DevEx | "I would be unhappy to lose access" (survey) | ≥ 60% agree |
| Cost | Fully loaded tool cost per engineer per month vs. hours saved | ROI ≥ 3x |

### 8.4 Guardrail Metrics (any breach triggers review)

- Security incident or data leak caused by AI tooling: **0 tolerated**.
- Secrets detected in AI-generated code reaching main: **0**.
- Change failure rate up by **more than 5 percentage points** on pilot teams.
- Developer satisfaction **below 3.0** for 2 consecutive pulses.
- Monthly spend more than **20% over budget**.

### 8.5 Go / No-Go Criteria (end of Month 6)

| Outcome | Criteria |
| --- | --- |
| **Scale** | ≥ 5 of 8 primary metrics hit target, all guardrails held, ROI ≥ 3x |
| **Adjust & Extend** | 3–4 primary metrics hit, guardrails held; narrow to the high-value use cases and extend 3 months |
| **Stop** | ≤ 2 primary metrics hit, or any guardrail breached without a fix |

## 9. Measurement Approach

- **Quantitative:** SCM analytics (e.g. GitHub/GitLab insights or a DORA tool), CI/CD data, issue tracker, security scanners, vendor usage telemetry.
- **Qualitative:** monthly pulse surveys (5 min), bi-weekly office hours, mid-point and end-point interviews with 10–15 participants.
- **Attribution:** label AI-assisted PRs (`ai-assisted`, `ai-agent`); compare pilot vs. comparison group; normalize for team size and sprint load.
- **Cadence:** weekly dashboard, monthly steering review, readouts at Month 3 (mid-point) and Month 6 (final).

## 10. Risks & Mitigations

| Risk | Likelihood | Impact | Mitigation |
| --- | --- | --- | --- |
| Code / IP leakage to vendor | Medium | High | Zero-retention contract, privacy mode, restricted-repo blocklist, Security review before kickoff |
| Lower code quality or subtle bugs | Medium | High | Mandatory human review, CI gates, SAST on all PRs, quality guardrail metrics |
| License-tainted generated code | Low | Medium | License/similarity filters, Legal guidance, OSS scanning |
| Low adoption / novelty wears off | Medium | Medium | Champions program, training, shared prompt library, regular use-case demos |
| Metrics noisy / hard to attribute | High | Medium | Baseline + comparison group, PR labeling, combine quantitative and qualitative data |
| Over-reliance / skill erosion (esp. juniors) | Medium | Medium | Review norms, pairing, "explain your change" expectation in PRs |
| Cost overrun from usage-based pricing | Medium | Medium | Budget caps, weekly spend tracking, usage alerts |
| Vendor lock-in | Low | Medium | Evaluate ≥ 2 vendors where feasible; avoid proprietary-only workflows |

## 11. Dependencies

- Security & Legal approval of vendor(s) (DPA, SOC 2 review, contract terms).
- Procurement and budget sign-off.
- IT/IdP integration (SSO, SCIM).
- Access to SCM/CI analytics data for baselining.
- Engineering managers committing pilot team capacity for training and feedback.

## 12. Budget (Estimate – fill in)

| Item | Estimate |
| --- | --- |
| Tool licenses (≈ 40–60 seats × 6 months) | _$TBD_ |
| Usage-based / agent compute costs | _$TBD (with monthly cap)_ |
| Analytics / DORA tooling (if not already owned) | _$TBD_ |
| Training & enablement time (~4 hrs per participant) | Internal time |
| Pilot team overhead (PM / analyst, partial) | Internal time |
| **Total** | _$TBD_ |

## 13. Open Questions

1. Which vendors are on the shortlist, and do we evaluate one or compare two head to head?
2. Which repositories are restricted (regulated data, crypto, customer PII)?
3. Do we have an existing engineering metrics platform, or do we need one?
4. Are contractors and offshore teams eligible to participate?
5. Who owns the AI usage policy long-term: Security, Legal, or the Platform team?

## 14. Approvals

| Role | Name | Status |
| --- | --- | --- |
| Executive Sponsor | _TBD_ | Pending |
| Engineering Leadership | _TBD_ | Pending |
| Security / CISO | _TBD_ | Pending |
| Legal / Privacy | _TBD_ | Pending |
| Finance / Procurement | _TBD_ | Pending |
