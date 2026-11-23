# Plan: 6-Month AI-Assisted Engineering Pilot

Companion to [PRD.md](./PRD.md). This document covers **who** is involved, **which teams** take part, and **how** the pilot runs month by month.

---

## 1. Pilot at a Glance

| Item | Detail |
| --- | --- |
| Duration | 26 weeks (Month 0 prep plus 6 pilot months) |
| Participants | ~40–60 engineers across 4–5 pilot teams |
| Comparison group | 2–3 teams with similar work that keep current tooling |
| Phases | Prepare & Baseline → Onboard → Expand → Scale Use Cases → Optimize → Evaluate & Decide |
| Key readouts | Month 3 mid-point review, Month 6 final go/no-go |

---

## 2. Stakeholders

### 2.1 Stakeholder Map

| Stakeholder | Role in Pilot | Interest | Influence | Engagement |
| --- | --- | --- | --- | --- |
| VP / Director of Engineering | **Executive Sponsor**: funds pilot, owns final decision | High | High | Monthly steering, final readout |
| Pilot Lead (Eddie) | **Driver**: runs the plan, metrics, comms | High | Medium | Daily / weekly |
| Engineering Managers (pilot teams) | Commit team capacity, collect feedback, report outcomes | High | Medium | Weekly sync |
| Tech Leads / Staff Engineers | Set review norms, identify use cases, act as champions | High | Medium | Weekly sync, office hours |
| Pilot Engineers | Daily users; give feedback and data | High | Low–Medium | Surveys, office hours, Slack channel |
| CISO / Security Engineering | Vendor security review, guardrails, incident response | Medium | High | Pre-launch approval, monthly review |
| Legal / Privacy / Compliance | Contract terms, IP and licensing, data processing | Medium | High | Pre-launch approval, as-needed |
| Procurement / Finance | Vendor contracts, budget tracking, ROI model | Medium | Medium | Pre-launch, monthly spend report |
| IT / Identity | SSO, SCIM, device and endpoint policies | Low | Medium | Setup phase |
| Platform / DevEx Team | Integrations, CI, telemetry, dashboards | High | Medium | Weekly |
| Product Management | Keeps roadmap commitments intact during pilot | Medium | Medium | Monthly update |
| HR / People / L&D | Training programs, change management, role-impact messaging | Low | Medium | Kickoff and final |
| Comparison-group EMs | Provide baseline data, no tool change | Low | Low | Monthly data pull |
| AI Vendor(s) | Technical support, enablement, roadmap insight | Medium | Low | Bi-weekly check-in |

### 2.2 RACI (key activities)

R = Responsible, A = Accountable, C = Consulted, I = Informed

| Activity | Exec Sponsor | Pilot Lead | EMs | Tech Leads | Security | Legal | Platform/DevEx | Finance |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| Vendor selection | A | R | C | C | C | C | C | C |
| Security & privacy approval | I | C | I | I | A/R | R | C | I |
| Contract & budget | A | C | I | I | C | R | I | R |
| Tool setup & integrations | I | A | I | C | C | I | R | I |
| Baseline & metrics dashboard | I | A | C | C | I | I | R | I |
| Training & enablement | I | A | C | R | C | I | C | I |
| Weekly operations & feedback | I | A/R | R | R | I | I | C | I |
| Guardrail monitoring | I | R | C | C | A | C | R | C (spend) |
| Mid-point & final readout | A | R | C | C | C | C | C | C |
| Go/no-go decision | A/R | C | C | C | C | C | I | C |

### 2.3 Governance

- **Steering Committee (monthly, 45 min):** Exec Sponsor, Pilot Lead, Security, a rotating EM, Finance. Reviews metrics, guardrails, budget, and blockers.
- **Working Group (weekly, 30 min):** Pilot Lead, pilot EMs/TLs, Platform/DevEx, Champions. Handles operations, feedback, and use-case tracking.
- **Champions Network:** 1–2 engineers per pilot team who run demos, share prompts and rules, and gather feedback.
- **Comms:** `#ai-pilot` Slack channel, bi-weekly digest email, monthly demo day.

---

## 3. Suggested Pilot Teams

Pick teams with a **mix of work types, tech stacks, and seniority** so results generalize. Each team should have an EM who supports the pilot and enough stable work to measure.

| # | Suggested Team | Size | Why This Team | Focus Use Cases |
| --- | --- | --- | --- | --- |
| 1 | **Product / Feature Team (Web or Mobile)** | 8–12 | High-volume feature work; clear PR and cycle-time signal | UC1 IDE assistant, UC2 tests, UC3 code review |
| 2 | **Backend / API Services Team** | 8–12 | Typed services, good test coverage; a good fit for agents | UC1, UC2, UC4 background agents |
| 3 | **Platform / DevEx / Infra Team** | 6–10 | Scripts, IaC, CI/CD; also owns integrations and telemetry | UC1, UC7 migrations, UC4 agents for chores |
| 4 | **QA / SDET / Test Automation** | 4–8 | Direct test-generation and flaky-test value | UC2 tests, UC3 review |
| 5 | **Legacy / Maintenance Team** (optional) | 6–10 | Tech debt, older codebase; tests AI on hard context | UC5 codebase Q&A, UC7 migrations, UC6 docs |
| — | **New Hire Cohort** (cross-team) | 3–6 | Measures onboarding impact | UC5 codebase Q&A, UC1 |

**Comparison group:** 2–3 teams similar to Teams 1–2 that keep current tooling for the whole pilot.

**Teams to avoid in the first wave:** teams on regulated or PII-heavy code (payments, health data, auth/crypto), teams in the middle of a major launch or reorg, and teams without CI/test coverage (too noisy to measure).

### 3.1 Core Pilot Team (operating team)

| Role | Allocation | Responsibilities |
| --- | --- | --- |
| Pilot Lead (Eddie) | ~50% | Plan, stakeholder management, metrics, readouts |
| Platform/DevEx Engineer | ~30% | SSO, repo access, telemetry, dashboards, PR labeling automation |
| Data / Eng Analytics Analyst | ~20% | Baseline, comparison-group analysis, ROI model |
| Security Partner | ~10% | Guardrails, scanning, incident playbook |
| Champions (1–2 per team) | ~10% each | Enablement, feedback, prompt and rules library |
| Program / Project Manager (optional) | ~25% | Scheduling, comms, tracking |

---

## 4. Timeline & Phases

```
Month:      M0        M1        M2        M3        M4        M5        M6
          |--Prep--|--Onboard--|--Expand--|--Mid-Pt--|--Scale--|--Optimize--|--Decide--|
Teams:              T1,T2      +T3,T4     review     +T5,NH     all        final
Readouts:                                 ★ Mid                            ★ Final
```

### Phase 0 — Prepare & Baseline (Weeks −4 to 0)

**Goal:** approvals, tooling, and baseline in place before any engineer gets access.

- [ ] Confirm Exec Sponsor and Steering Committee; approve PRD.
- [ ] Shortlist vendors (1 primary, optionally 1 for comparison); run demos and trials.
- [ ] Security review (SOC 2, DPA, zero retention); Legal review (IP, licensing).
- [ ] Procurement: contracts, seat counts, usage caps.
- [ ] Publish an **AI Acceptable Use Policy** (approved repos, data rules, review rules).
- [ ] IT: SSO/SCIM setup; Platform: repo allowlist, PR labels, telemetry export.
- [ ] Pull **3 months of historical baseline** (cycle time, DORA, defects, coverage).
- [ ] Run the **pre-pilot survey** (developer experience, current AI usage, pain points).
- [ ] Select pilot teams and comparison group; name champions.

**Exit criteria:** security and legal sign-off, baseline dashboard live, teams confirmed.

### Phase 1 — Onboard Wave 1 (Month 1)

**Goal:** get Teams 1 and 2 productive and the telemetry flowing.

- Kickoff session; 2-hour hands-on training per team (prompting, context, review norms).
- Turn on UC1 (IDE assistant) and UC3 (AI code review).
- Set up `#ai-pilot`, office hours (2x weekly), and a shared prompt/rules repo.
- Weekly working group; first pulse survey at end of month.

**Exit criteria:** ≥ 60% weekly active in Wave 1; telemetry validated; no security issues.

### Phase 2 — Expand Wave 2 (Month 2)

**Goal:** add Teams 3 and 4 and introduce agents and test generation.

- Onboard Platform/DevEx and QA teams.
- Turn on UC2 (test generation) and UC4 (background agents) for scoped ticket types (bugs, chores, small features) with a ticket label such as `agent-eligible`.
- Document the agent workflow: ticket → agent → PR → human review → merge.
- Monthly demo day: champions show wins and failures.

**Exit criteria:** agents completing tickets end to end; review norms documented.

### Phase 3 — Mid-Point Review (Month 3)

**Goal:** check direction with data.

- Analyze pilot vs. baseline vs. comparison group on all primary metrics.
- 10–15 participant interviews; mid-point survey.
- **Steering readout:** continue, adjust use cases, or stop early if guardrails were breached.
- Re-prioritize use cases: double down on high-value ones, drop low-value ones.

**Exit criteria:** steering committee decision recorded; adjusted plan published.

### Phase 4 — Scale Use Cases (Month 4)

**Goal:** broaden coverage and test harder scenarios.

- Onboard Team 5 (Legacy) and the New Hire cohort.
- Turn on UC5 (codebase Q&A/onboarding), UC6 (docs), UC7 (migrations).
- Run 1–2 **targeted campaigns**, e.g. a dependency upgrade or a test-coverage push done mostly by agents.
- Grow the shared rules library into team-specific conventions.

**Exit criteria:** all use cases active; campaign results measured.

### Phase 5 — Optimize (Month 5)

**Goal:** improve efficiency and get the scale-out ready.

- Tune usage: find power users, help low adopters, refine agent ticket criteria.
- Cost analysis: usage patterns, spend per engineer, cost per merged agent PR.
- Draft the **rollout playbook**: onboarding guide, training curriculum, policy, support model.
- Draft the org-wide cost model and vendor recommendation.

**Exit criteria:** draft rollout playbook and ROI model reviewed by the working group.

### Phase 6 — Evaluate & Decide (Month 6)

**Goal:** final evaluation and go/no-go decision.

- Final data pull and analysis against the PRD Section 8 targets.
- Final survey and interviews.
- **Final readout to Steering Committee** using the go/no-go criteria (Scale / Adjust & Extend / Stop).
- If Scale: approve the rollout plan, budget, and phased timeline.
- If Stop: offboarding plan, revoke access, document lessons learned.
- Publish the pilot retrospective.

**Exit criteria:** decision recorded; next-step plan funded or pilot closed.

---

## 5. Milestones

| Week | Milestone | Owner |
| --- | --- | --- |
| W−4 | PRD approved, sponsor confirmed | Pilot Lead |
| W−2 | Security & Legal sign-off | Security / Legal |
| W0 | Baseline dashboard live; teams selected | Platform / Analyst |
| W1 | Pilot kickoff; Wave 1 onboarded | Pilot Lead |
| W4 | First pulse survey; Month 1 report | Pilot Lead |
| W5 | Wave 2 onboarded; agents enabled | Platform / EMs |
| W13 | **Mid-point readout** | Pilot Lead → Steering |
| W17 | Wave 3 onboarded; campaigns start | Pilot Lead / EMs |
| W22 | Draft rollout playbook and ROI model | Pilot Lead / Analyst |
| W26 | **Final readout and go/no-go** | Exec Sponsor |

---

## 6. Enablement & Change Management

- **Training:** 2-hour onboarding workshop; 30-minute advanced sessions each month (agents, context and rules, reviewing AI code).
- **Resources:** internal wiki page, prompt and rules library, a "good AI PR" example gallery.
- **Support:** office hours twice a week, `#ai-pilot` channel, a champion on every team.
- **Messaging:** position the pilot as augmentation, not replacement. Be open about what is measured; metrics are used at **team level, never for individual performance reviews**.
- **Recognition:** monthly "best use case" showcase at demo day.

---

## 7. Reporting Cadence

| Report | Audience | Frequency | Contents |
| --- | --- | --- | --- |
| Metrics dashboard | All stakeholders | Live / weekly | Adoption, cycle time, DORA, guardrails |
| Working group notes | Pilot teams | Weekly | Blockers, feedback, actions |
| Pilot digest | Broader engineering | Bi-weekly | Wins, tips, upcoming changes |
| Steering update | Steering Committee | Monthly | Metrics vs. targets, risks, spend |
| Mid-point readout | Steering + Eng leadership | Month 3 | Full analysis, adjust/continue |
| Final readout | Exec Sponsor + leadership | Month 6 | Go/no-go, rollout plan, ROI |

---

## 8. Risk Response Playbook

| Trigger | Response | Owner |
| --- | --- | --- |
| Security incident or data exposure | Pause tool access immediately; run incident response; Steering notified within 24h | Security |
| Guardrail metric breached | Root-cause within 1 week; corrective plan or scope reduction | Pilot Lead |
| Adoption < 50% for 2 weeks | Champion intervention, targeted training, survey for blockers | EMs / Champions |
| Spend > 20% over budget | Apply usage caps; review agent usage; Finance notified | Pilot Lead / Finance |
| Vendor outage or major regression | Fall back to standard workflow; log impact; vendor escalation | Platform |

---

## 9. Next Steps (this week)

1. Share PRD and plan with the prospective Exec Sponsor for feedback.
2. Book an intro meeting with Security and Legal to start the vendor review.
3. Confirm candidate pilot teams with their EMs.
4. Ask the Platform/DevEx team about available engineering metrics data for the baseline.
5. Fill in the TBDs in PRD Section 12 (Budget) and Section 13 (Open Questions).
