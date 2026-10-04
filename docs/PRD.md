# Website Testing Engine — Product Requirements Document

> **Document:** `docs/PRD.md`
> **Product:** Website Testing Engine (WTE)
> **Product class:** Universal Autonomous Software Testing & Quality Intelligence Platform
> **Document status:** Authoritative product definition (North Star)
> **Version:** 1.0.0
> **Owner:** Product Architecture
> **Applies to:** the WTE platform as a whole
> **Last updated:** 2026-10-04

---

## 1. Document Purpose

### 1.1 What this document is

This document is the authoritative product definition for the **Website Testing Engine (WTE)**.

It defines:

- **What WTE is** — as a product, as a category of software, and as a long-term platform.
- **Why WTE exists** — the problems it is created to solve and the value it must deliver.
- **Who WTE is for** — the people and organizations whose work it must improve.
- **What WTE must ultimately be able to test** — the universal target and testing taxonomy the product model must be able to represent.
- **What product capabilities WTE must expose** — capability by capability, expressed independently of vendors.
- **How users experience and control those capabilities** — journeys, authorization, safety, and explainability.
- **How raw testing evidence becomes quality intelligence** — evidence, findings, correlation, root cause, scoring, release readiness, history, and learning.
- **What is explicitly outside WTE's responsibility** — so that boundaries with engines, tools, and the user's organization remain unambiguous.
- **What is current, foundational, planned, and long-term** — with no overclaiming.

This PRD is the **North Star for the product**. It is the reference used to judge whether a proposed feature, engine, integration, or architectural change belongs in WTE, and what problem it must solve.

### 1.2 What this document is not

This PRD is **not** an implementation specification. It deliberately avoids prescribing:

- programming languages, frameworks, databases, queues, or deployment topology;
- specific vendors for any capability;
- schema, table, or API designs;
- internal module structure.

Those belong to the sibling documents listed in §1.5. Requirements in this document are written in product language: they describe **observable platform behavior and product guarantees**, not internal mechanisms.

### 1.3 Repository state at authoring time (honesty statement)

At the time this document was written, the repository contained only a `LICENSE` file. No `/docs` directory, no application code, no packages, engines, workers, adapters, or tests existed.

Consequences for how this document must be read:

- **Nothing in this document is `CURRENT`.** No capability described here is implemented today.
- Every capability is expressed as a product requirement with an explicit horizon (`FOUNDATIONAL`, `PLANNED`, `LONG-TERM`, or `EXTENSION`).
- Requirement identifiers (§1.6) exist so future work — including `PHASES.md`, `ARCHITECTURE.md`, and `CHANGELOG.md` — can trace back to product intent.
- Any future claim of implementation must be backed by repository evidence, not by this document.

This honesty rule is itself a product requirement (§6, P18).

### 1.4 Status and horizon vocabulary

| Label | Meaning |
|---|---|
| **CURRENT** | Implemented in the repository and verifiable by code, tests, or delivered documentation. |
| **FOUNDATIONAL** | Required first platform primitives. Everything else depends on these. Not implemented yet. |
| **PLANNED** | Committed product scope for a defined horizon; expected to be built on top of the foundation. |
| **LONG-TERM** | Directionally committed; depends on foundational and planned layers being mature. |
| **EXTENSION** | Supported by an explicit extensibility model; not built by WTE itself until demand and safety justify it. |
| **TBD** | A value, target, or decision that is deliberately not fixed in this document. Must be resolved before the relevant capability is declared generally available. |

Rules:

1. A capability is never described as available unless it exists in the repository.
2. Numeric targets are never invented. Undecided numbers are marked `TBD`.
3. Where a requirement is future work, this document says so in place, not just in a summary.

### 1.5 Document map — what lives where

This PRD does not duplicate other documentation. The division of responsibility is:

| Document | Responsibility |
|---|---|
| `docs/PRD.md` (this document) | **What** WTE is, **why** it exists, and the **product requirements** it must satisfy. |
| `docs/ARCHITECTURE.md` | **How** the platform is structured: components, engines, data flow, deployment topology. |
| `docs/RULES.md` | Non-negotiable engineering invariants and constraints. |
| `docs/DESIGN.md` | User experience, interaction design, information architecture, visual language. |
| `docs/PHASES.md` | Implementation order and phase composition. |
| `docs/DATABASE.md` | Persistence model. |
| `docs/API.md` | External and internal contracts. |
| `docs/SECURITY.md` | Detailed trust, permission, and threat model. |
| `docs/TESTING.md` | How WTE itself is verified. |
| `docs/DEPLOYMENT.md` | How WTE runs in environments. |
| `docs/CHANGELOG.md` | What has actually been delivered. |

At authoring time, none of these sibling documents existed. This PRD defines the product boundaries they will inherit, and §40 lists open questions that must be resolved in them.

### 1.6 Requirement identifiers

Significant product requirements carry stable identifiers of the form:

```
WTE-PRD-<AREA>-<NNN>
```

Examples: `WTE-PRD-CORE-001`, `WTE-PRD-A11Y-004`, `WTE-PRD-RCA-002`.

Identifier rules:

- IDs are **stable**; they are never reused or renumbered.
- IDs are assigned only to meaningful product requirements, never to prose.
- A requirement may be **refined** over time (clarified, split, or superseded), but the original ID remains resolvable.
- Requirements that are removed are marked **SUPERSEDED** with a pointer to their replacement, never silently deleted.

Area prefixes used in this document:

| Prefix | Area | Prefix | Area |
|---|---|---|---|
| `CORE` | Platform fundamentals and product model | `EVID` | Evidence |
| `TARGET` | Targets and environments | `FIND` | Findings |
| `AUTH` | Authorization and safe execution | `CORR` | Correlation |
| `DISC` | Discovery and reconnaissance | `RCA` | Root-cause intelligence |
| `KNOW` | Application knowledge | `HIST` | Historical intelligence |
| `BROWSER` | Browser automation | `IMPACT` | Change impact analysis |
| `FUNC` | Functional and business logic | `SELECT` | Intelligent test selection |
| `UIUX` | UI and UX | `GEN` | Test generation |
| `VISUAL` | Visual and computer vision | `FLAKY` | Flaky test intelligence |
| `A11Y` | Accessibility | `HEAL` | Self-healing |
| `COMPAT` | Responsive and compatibility | `QUAL` | Quality model |
| `API` | APIs, protocols, and contracts | `REL` | Release readiness |
| `IDENT` | Authentication, authorization, session | `REPORT` | Reporting |
| `SEC` | Security testing and application security | `DASH` | Dashboards |
| `PRIV` | Privacy | `INTEG` | Integrations |
| `PERF` | Performance | `ORCH` | Execution and orchestration |
| `LOAD` | Load and scalability | `NFR` | Non-functional requirements |
| `NET` | Network, DNS, TLS, edge | `METRIC` | Product success metrics |
| `DB` | Database | `EXT` | Extensibility |
| `DATA` | Data quality and pipelines | `PLAT` | Testing the testing platform |
| `MSG` | Email and notifications | `SEO` | SEO and content |
| `I18N` | Localization and internationalization | `PWA` | PWA and service workers |
| `PAY` | Payments | `MOBILE` | Mobile |
| `ECOM` | E-commerce | `DESKTOP` | Desktop |
| `BUILD` | Build and code quality | `CICD` | CI/CD |
| `INFRA` | Containers, Kubernetes, IaC | `CLOUD` | Cloud and serverless |
| `RELIAB` | Reliability engineering | `CHAOS` | Chaos engineering |
| `DR` | Disaster recovery | `OBS` | Observability and monitoring |
| `SLO` | SLO/SLA validation | `AI` | AI, ML, LLM, RAG, agents |

### 1.7 Audience

| Audience | How to use this document |
|---|---|
| Product and architecture | The source of truth for scope decisions and the North Star. |
| Engineering | The intent behind every capability; implementation constraints come from `RULES.md` and `ARCHITECTURE.md`. |
| QA and testing practitioners | The definition of what the platform will be able to test and how results become intelligence. |
| Security and compliance | The product-level safety and authorization guarantees WTE must honor. |
| Design | The journeys, personas, and information needs the UX must satisfy. |
| Leadership | The product definition, horizons, success metrics, and risks. |
| Contributors and integrators | How capabilities, engines, adapters, and integrations are expected to fit together. |

---

## 2. Product Vision

### 2.1 Vision statement

> **WTE is an autonomous, evidence-driven software testing and quality intelligence platform.** It discovers authorized software systems, understands their structure, dependencies, and behavior, determines the quality risks that matter for those systems, selects and safely executes the appropriate testing capabilities, collects normalized evidence, correlates symptoms into meaningful findings, identifies probable root causes, evaluates multidimensional quality, and determines release readiness — learning from every run and improving the next one.

### 2.2 The long-term ambition

WTE should eventually be able to look at an authorized software system, understand what it is and how it works, reason about what can fail, determine how those risks should be tested, execute the right testing safely, collect the evidence, diagnose the failures, explain the system's quality, and state — with justification — whether the system is ready to release.

That ambition is bounded by two permanent commitments:

1. **WTE never operates outside explicit authorization.**
2. **WTE never asks the user to trust an AI opinion that is not grounded in evidence.**

### 2.3 Why the name stays

The historical project name is **Website Testing Engine**, reflecting its origin: understanding and testing web systems. The product has outgrown that name.

The name is retained for continuity of the project, the platform, and the brand. The **product definition** is universal: WTE is a platform for testing and quality intelligence across software systems generally, with web and browser-based systems as its foundational strength and evolutionary starting point.

The name is a historical artifact, not a scope limitation.

---

## 3. Problem Statement

### 3.1 The state of software quality practice today

Modern software systems are distributed, dynamic, multi-layered, and continuously changing. Quality practice has not kept pace. The dominant patterns are:

1. **Fragmentation.** Testing is spread across dozens of tools — browser automation, API clients, accessibility scanners, performance profilers, load generators, security scanners, database checks, observability dashboards. Each tool has its own configuration, execution model, output format, and vocabulary.
2. **Evidence silos.** A single production-quality failure may appear simultaneously as a browser error, a console exception, a failed HTTP call, an empty chart, a failed assertion, and a spike in a metric. Each of these lands in a different system. No one correlates them.
3. **Disconnection from risk.** Test suites grow by accretion, not design. Teams run everything, or run what they ran last time, or run what is cheap to run — instead of running what the change actually put at risk.
4. **Manual correlation and diagnosis.** Engineers spend significant time manually reproducing failures, collecting artifacts across systems, and guessing at root causes.
5. **Opinion-driven release decisions.** Release readiness is frequently determined by whether a pipeline went green, not by an evidence-based assessment of risk across functional, security, performance, accessibility, reliability, and data dimensions.
6. **No learning across runs.** Runs are events, not history. The platform rarely knows whether a failure is new, recurring, flaky, or a known accepted risk.
7. **Tool-bound capabilities.** Teams think in terms of the tools they have rather than the capabilities they need. When the tool changes, the knowledge built around it is lost.
8. **AI without grounding.** New AI-assisted testing tools generate plausible-sounding conclusions without deterministic evidence, and agentic systems browse untrusted content without adequate authorization models or prompt-injection defenses.

### 3.2 The cost

The consequences are consistent and expensive:

- Regressions reach production that a targeted test would have caught.
- Critical workflows are under-tested while low-value tests dominate execution time.
- Findings are duplicated, mis-prioritized, and eventually ignored.
- Release decisions cannot be explained after the fact.
- Quality data cannot be compared across releases because baselines were never established.
- Security, accessibility, and performance issues are discovered late, when remediation is most expensive.
- Engineers distrust quality signals and route around them.

### 3.3 Why a new category of platform is needed

Point tools solve point problems and will continue to exist. The gap is not another scanner or another runner. The gap is a **platform layer** that:

- knows the target system as a system, not as a URL;
- turns testing capabilities into a coherent, vendor-neutral registry;
- enforces authorization, scope, and safety as first-class product behavior;
- normalizes every observation into one evidence model;
- converts evidence into deduplicated, correlated findings;
- reasons about root cause with evidence, not opinion;
- scores quality across dimensions and determines release readiness;
- and accumulates history so that every run makes the platform smarter.

That platform layer is WTE.

---

## 4. Product Definition

### 4.1 Definition

> **WTE is an autonomous, evidence-driven software testing and quality intelligence platform that discovers systems, understands their structure and behavior, models their dependencies, determines relevant quality risks, selects appropriate testing capabilities, safely executes tests through specialized engines, collects normalized evidence, correlates symptoms into meaningful findings, identifies probable root causes, evaluates multidimensional quality, and determines release readiness.**

### 4.2 The product in one operating loop

```
TARGET
   ↓
AUTHORIZE
   ↓
DISCOVER
   ↓
UNDERSTAND
   ↓
MODEL
   ↓
IDENTIFY RISKS
   ↓
PLAN TESTING
   ↓
SELECT CAPABILITIES
   ↓
SELECT ENGINES
   ↓
EXECUTE
   ↓
OBSERVE
   ↓
COLLECT EVIDENCE
   ↓
NORMALIZE
   ↓
EVALUATE
   ↓
CORRELATE
   ↓
CREATE FINDINGS
   ↓
DETERMINE ROOT CAUSE
   ↓
ASSESS IMPACT
   ↓
ASSESS RISK
   ↓
SCORE QUALITY
   ↓
DETERMINE RELEASE READINESS
   ↓
STORE HISTORY
   ↓
LEARN
   ↓
IMPROVE NEXT RUN
```

Every stage is a **product responsibility**. Every stage must produce something the next stage can consume, and something a human can inspect.

### 4.3 Product archetype

```
                        SOFTWARE / SYSTEM
                              │
                              ↓
                       WTE ORCHESTRATOR
                              │
             ┌────────────────┼────────────────┐
             │                │                │
        UNDERSTAND          DECIDE          CONTROL
             │                │                │
       Discovery          Risk/Test       Authorization
       Knowledge          Planning        Permissions
             │                │                │
             └────────────────┼────────────────┘
                              ↓
                     CAPABILITY REGISTRY
                              │
      ┌───────────────────────┼───────────────────────┐
      │                       │                       │
     WEB                  PLATFORM               INTELLIGENCE
      │                       │                       │
 Browser                Infrastructure               AI
 Functional             Cloud                        RCA
 UI/UX                  Data                         Risk
 Visual                 Mobile                       Healing
 Accessibility          Desktop                      Selection
 API                    Reliability                  Generation
 Security               Observability                Quality
 Performance
      │                       │                       │
      └───────────────────────┼───────────────────────┘
                              ↓
                       EXECUTION LAYER
                              ↓
                            EVIDENCE
                              ↓
                           FINDINGS
                              ↓
                          CORRELATION
                              ↓
                         ROOT CAUSE
                              ↓
                       QUALITY / RISK
                              ↓
                     RELEASE READINESS
                              ↓
                           HISTORY
                              ↓
                           LEARNING
```

### 4.4 The product is not a collection of wrappers

WTE is explicitly **not** any of the following, and must never degrade into them:

| WTE is not | Why the distinction matters |
|---|---|
| A browser automation framework | Browser automation is one capability among many, behind a vendor-neutral registry. |
| An end-to-end test runner | Running tests is a stage of the loop, not the product. |
| An accessibility scanner | Accessibility is one quality dimension in a multidimensional model. |
| A vulnerability scanner | Security testing is one authorized capability family, not the product identity. |
| A performance or load-testing tool | Performance evidence contributes to quality and release readiness; it does not define the platform. |
| An API client | API testing is one family of capabilities feeding one evidence model. |
| A collection of CLI wrappers | Wrapping tools without normalization, correlation, or intelligence creates no durable value. |
| "AI around Playwright" | AI is an intelligence layer over deterministic evidence, not a replacement for it. |
| A report generator | Reports are the surface of a quality model, not the product. |
| A testing dashboard | Dashboards visualize intelligence; they do not constitute it. |
| An LLM chatbot | Conversational access is an interface; it is not the product and it is never the source of truth. |

> `WTE-PRD-CORE-001` — WTE must coordinate and unify testing capabilities through a common quality platform rather than acting as a standalone tool, runner, scanner, or wrapper collection.

### 4.5 The single most important platform principle

> **Do not build hundreds of disconnected testing tools.**

The product must converge on, and expose to users as one coherent system:

```
ONE WTE ORCHESTRATOR
+ ONE CAPABILITY / TOOL REGISTRY
+ ONE AUTHORIZATION & PERMISSION SYSTEM
+ ONE TARGET & ENVIRONMENT MODEL
+ ONE EXECUTION MODEL
+ ONE APPLICATION KNOWLEDGE MODEL
+ ONE EVIDENCE MODEL
+ ONE FINDING MODEL
+ ONE HISTORICAL INTELLIGENCE MODEL
+ ONE ROOT-CAUSE MODEL
+ ONE QUALITY MODEL
+ ONE RELEASE MODEL
+ ONE REPORTING MODEL
```

Specialized tools connect to these models through controlled engines, adapters, and plugins. A new tool must never create a new silo.

> `WTE-PRD-CORE-002` — Every capability, engine, and integration must read from and write to the shared platform models. Parallel, capability-specific data models are prohibited at the product level.

### 4.6 Core product guarantees

WTE must be able to make all of the following guarantees to its users. These are product-level commitments; their realization is spread across the requirements in this document.

| Guarantee | Statement |
|---|---|
| **Authorization** | No operation executes against a target that is not explicitly authorized for that class of operation. |
| **Scope integrity** | Operations remain inside declared scope boundaries; scope is verifiable and auditable. |
| **Safety by default** | The default behavior of every capability is the least invasive behavior that can satisfy the request. |
| **Evidence grounding** | Every actionable finding references supporting evidence wherever evidence exists. |
| **Explainability** | Every score, gate, and AI conclusion can be decomposed into the inputs that produced it. |
| **Determinism first** | Reliable deterministic checks are used wherever they exist, before probabilistic reasoning is applied. |
| **History** | Runs are comparable, baselines exist, and trends are derivable. |
| **Vendor independence** | Capabilities are defined independently of tools; tools are interchangeable behind adapters. |
| **Extensibility** | New testing domains can be added without redesigning the platform or redefining core models. |
| **Honesty** | The platform never presents unimplemented, unverified, or unsupported claims as facts. |

---

## 5. Why WTE Exists

### 5.1 The purpose

WTE exists to close the gap between **the testing a system needs** and **the quality understanding its owners actually have**.

It exists because:

1. **Software quality is multidimensional, and practice is one-dimensional.** Functional correctness, accessibility, performance, security, reliability, data integrity, compatibility, and AI behavior all matter. Teams measure whichever dimension their tools happen to cover.
2. **Testing capacity is finite and risk is not uniform.** Running everything is neither affordable nor meaningful. The platform must know what changed, what is critical, what has been fragile, and what deserves attention now.
3. **Evidence without correlation is noise.** Hundreds of raw observations do not equal understanding. Correlation, deduplication, and root-cause reasoning are what turn observation into action.
4. **Release decisions require justification.** "The pipeline is green" is not a risk assessment. Release readiness must be explainable, evidence-backed, and auditable.
5. **Autonomy requires trust, and trust requires control.** An autonomous testing agent that can browse, execute, and mutate is powerful and dangerous. WTE exists to make that power safe, scoped, permissioned, and reversible.
6. **Quality knowledge must compound.** Every run should make the platform better at knowing this system: its structure, its flakiness, its history, its risk areas, its baselines.

### 5.2 The value WTE must deliver

| Value | Description |
|---|---|
| **Discover what matters** | Automatically understand a target system's surface, structure, dependencies, and workflows. |
| **Test what matters** | Select capabilities and tests based on risk, change, criticality, history, and cost. |
| **Explain failures** | Correlate multi-source evidence into probable causes with confidence. |
| **Prove quality** | Evaluate quality across explainable dimensions with evidence, never with opaque scores alone. |
| **Decide releases** | Produce defensible READY / CONDITIONALLY READY / NOT READY outcomes with complete reasoning. |
| **Learn continuously** | Accumulate history that makes future testing cheaper, sharper, and more predictive. |
| **Stay safe** | Make every powerful operation authorization-gated, auditable, and blast-radius-limited. |
| **Stay open** | Never lock the customer's quality strategy to a single vendor. |

---

## 6. Product Principles

These principles are permanent. They apply to every capability in this document. Where a future requirement conflicts with a principle, the conflict must be resolved explicitly — never silently ignored.

**P1 — One platform, one model.** Do not build hundreds of disconnected testing tools. All capability flows through one orchestrator, one registry, one target model, one evidence model, one finding model, one quality model.

**P2 — Capability-first, vendor-neutral.** The product defines capabilities; tools are interchangeable implementations behind engines and adapters. No product requirement may permanently bind WTE to a vendor.

**P3 — Observation before judgment.** Extractors observe; evaluators judge. Never mix raw observation with subjective evaluation. `OBSERVE → NORMALIZE → EVALUATE → CORRELATE → REPORT` is the permanent pipeline order.

**P4 — Deterministic systems before AI judgment.** AI operates over evidence. Reliable deterministic validation is preferred wherever it exists. AI is used for planning, correlation, classification, reasoning, prioritization, and recommendation — not as a substitute for deterministic checks.

**P5 — Evidence is first-class.** Every meaningful result can produce normalized, stored, secure, referenceable evidence. Findings point to evidence. AI conclusions point to evidence where possible.

**P6 — Concept discipline.** Domain ≠ category ≠ capability ≠ engine ≠ tool. Confusing these layers is a design defect.

**P7 — Taxonomy is not architecture.** The testing taxonomy describes risks and capabilities to represent — not the number of engines, packages, or workers to build.

**P8 — Authorization is a product feature.** Risk classification, scope boundaries, environment awareness, and permission checks are part of the product surface, not an afterthought.

**P9 — Untrusted content stays untrusted.** Browsed websites, API responses, documents, and application text are data. They are never instructions, never grant permissions, and never override platform rules.

**P10 — Distinguish observation, symptom, finding, root cause, and recommendation.** These are different things with different lifecycles, confidence levels, and owners. They must never be used interchangeably.

**P11 — Deduplicate aggressively; correlate fearlessly.** Many symptoms, one cause. The platform's value is in reduction, not accumulation.

**P12 — Explain or don't conclude.** A score, gate, or conclusion that cannot be explained must not be presented as authoritative.

**P13 — History is an asset.** Runs are comparable artifacts, not disposable events. Baselines, trends, and recurrence are first-class data.

**P14 — Safe by default, powerful on request.** Least-invasive behavior is the default. Dangerous operations require explicit, scoped, justified authorization.

**P15 — Autonomy is earned in stages.** Automatic discovery → automatic planning → automatic execution → automatic investigation. Each stage introduces increasing requirements for auditability, reversibility, and confidence.

**P16 — No silent mutation, ever.** Any change WTE makes to a target, an environment, or its own configuration is explicit, logged, versioned, and reversible where feasible.

**P17 — Extensibility is structural.** New domains, capabilities, engines, and adapters must be addable without redesigning core models.

**P18 — Honesty about state.** The product and its documentation never claim implemented capability without evidence. "Planned", "future", and `TBD` are acceptable answers; false confidence is not.

**P19 — Boundaries are explicit.** WTE responsibility, external engine responsibility, and user/organization responsibility are always separable and documented.

**P20 — The platform must be testable by itself.** WTE's own engines, adapters, rules, evaluators, and decisions must be verifiable by WTE. No testing system may assume its own correctness.

---

## 7. Goals

### 7.1 Product goals

| ID | Goal |
|---|---|
| `G-1` | **Unify testing under one platform.** Provide one coherent place where discovery, planning, execution, evidence, findings, quality, and release readiness live together. |
| `G-2` | **Understand targets automatically.** Reduce the manual effort required to know what a system contains, how it is structured, and what depends on what. |
| `G-3` | **Test based on risk, not habit.** Make test selection driven by change, criticality, history, and dependency — not by "run everything". |
| `G-4` | **Turn evidence into understanding.** Systematically convert observations into deduplicated findings and evidence-backed probable causes. |
| `G-5` | **Make quality measurable and explainable.** Evaluate quality across dimensions with transparent inputs and no opaque scoring. |
| `G-6` | **Make release readiness defensible.** Produce release verdicts that can be explained line by line from evidence and policy. |
| `G-7` | **Reduce noise.** Aggressively deduplicate findings and identify flaky, recurring, and known-accepted failures. |
| `G-8` | **Compound knowledge over time.** Make every run improve the platform's model of the system and its predictions. |
| `G-9` | **Enable safe autonomy.** Allow increasingly autonomous operation while preserving authorization, scope, auditability, and reversibility. |
| `G-10` | **Remain vendor-independent.** Ensure customers can change tools without changing their quality platform. |
| `G-11` | **Cover the universal testing universe progressively.** Represent, plan, and eventually execute across the full taxonomy in §13 — without building one engine per category. |
| `G-12` | **Be trustworthy infrastructure.** Be reliable, observable, portable, and safe enough to run inside enterprises, regulated environments, and CI systems. |

### 7.2 Success conditions

The product goals are met when:

- a new target can be onboarded, discovered, and tested with minimal manual configuration;
- failures arrive pre-correlated, deduplicated, and evidence-backed;
- engineers trust the platform's findings enough to act on them without re-deriving them;
- release decisions reference specific evidence and policy, and can be audited after the fact;
- adding a new tool, engine, or testing domain does not require changing the product model;
- and nothing the platform does can occur outside an explicitly authorized scope.

---

## 8. Non-Goals

Non-goals are as important as goals. They define the boundary of the product.

| ID | Non-goal | Rationale |
|---|---|---|
| `NG-1` | **WTE is not a clone of every testing vendor.** | WTE integrates, normalizes, and reasons. Reimplementing every tool is not the product. |
| `NG-2` | **WTE is not an unrestricted penetration-testing platform.** | Security testing is authorization-gated and scope-bound, never an open attack tool. |
| `NG-3` | **WTE is not an unrestricted remote command shell.** | Execution targets specific capabilities against specific authorized scope. |
| `NG-4` | **WTE does not automatically attack public targets.** | A public URL never implies authorization. |
| `NG-5` | **WTE does not automatically stress public systems.** | Load generation requires explicit authorization and blast-radius controls. |
| `NG-6` | **WTE does not silently mutate production systems.** | Any mutation is explicit, scoped, logged, and (where feasible) reversible. |
| `NG-7` | **WTE does not store plaintext secrets.** | Secrets are referenced, never embedded in configuration, evidence, or reports. |
| `NG-8` | **WTE does not treat AI opinions as evidence.** | AI output is reasoning over evidence; it is not itself evidence. |
| `NG-9` | **WTE does not automatically declare legal compliance.** | It produces technical compliance evidence; legal conclusions belong to the organization and its counsel. |
| `NG-10` | **WTE does not require one vendor for every capability.** | Vendor lock-in contradicts `P2`. |
| `NG-11` | **WTE does not create one engine per testing category.** | Engine composition follows architecture, not taxonomy. |
| `NG-12` | **WTE does not claim certification for safety-critical systems.** | Domain adapters can produce evidence; certification bodies certify. |
| `NG-13` | **WTE is not a monitoring-only APM replacement.** | Monitoring is a monitoring system's job; WTE can consume and correlate its signals. |
| `NG-14` | **WTE is not a source code host, issue tracker, or CI system.** | It integrates with them; it does not replace them. |
| `NG-15` | **WTE is not a model training platform.** | AI/ML testing evaluates other systems' models; WTE does not train general-purpose models. |

> `WTE-PRD-CORE-003` — WTE must not implement any capability that violates the non-goals above, regardless of user request, configuration, or agent instruction.

---

## 9. Target Users

### 9.1 Persona families

WTE serves individual practitioners, teams, and enterprises. The persona families below are grouped by the problem they bring to the platform.

| # | Persona | Primary problem | Primary goal | Typical workflow | Required WTE capability |
|---|---|---|---|---|---|
| 1 | **Individual developer** | Verifying a change without building a full test harness. | Fast, trustworthy confirmation that a change works. | Change code → run targeted validation → inspect failures. | Change validation journey (§12.2), evidence, findings, local execution. |
| 2 | **Frontend engineer** | UI regressions, responsiveness, browser differences. | Confidence that the UI behaves and renders correctly. | Feature branch → browser/visual/accessibility checks → fix. | Browser engine, visual testing, responsive/compatibility, UI/UX rules. |
| 3 | **Backend engineer** | API regressions, contract breaks, performance drift. | Confidence that services behave and stay compatible. | Change service → API/contract/performance checks → diagnose. | API engine, contract & schema testing, performance, correlation with logs/traces. |
| 4 | **Full-stack engineer** | Cross-layer failures spanning UI, API, and data. | End-to-end diagnosis of multi-layer defects. | Change feature → end-to-end workflow run → correlated diagnosis. | Workflow testing, application knowledge graph, cross-layer correlation. |
| 5 | **QA engineer** | Manual effort spent on repetitive verification; evidence scattered. | Systematic, repeatable, evidence-backed verification. | Plan → execute suites → triage findings → verify fixes. | Test management, evidence model, findings, history, reporting. |
| 6 | **SDET / Automation engineer** | Fragile suites, selector churn, flakiness eroding trust. | Durable automation with low maintenance cost. | Author tests → run in CI → triage flaky failures → repair. | Test generation, flaky intelligence, self-healing (audited), coverage. |
| 7 | **Performance engineer** | Regression detection and performance budgets. | Reproducible performance evidence and regressions caught early. | Baseline → benchmark → compare → diagnose. | Performance engine, Core Web Vitals, performance budgets, history/baselines. |
| 8 | **Security engineer** | Validating controls inside authorized scope without uncontrolled scanners. | Authorized, scoped, auditable security validation. | Define scope → authorize class → run passive/active checks → review evidence. | Security engine, authorization model, evidence, findings, report/SARIF export. |
| 9 | **DevOps engineer** | Deployment validation and pipeline integration. | Automated post-deploy verification and rollback confidence. | Pipeline stage → deployment validation → gate → promote/rollback. | CI/CD integration, deployment testing, release readiness, quality gates. |
| 10 | **Platform engineer** | Standardizing quality across many teams and services. | A shared, governed quality platform. | Configure targets, policies, capability sets, reports across teams. | Multi-project model, capability registry, policies, dashboards, integrations. |
| 11 | **SRE** | Reliability regressions, SLO validation, incident context. | Evidence-based reliability assurance and faster incident diagnosis. | Continuous verification → alert correlation → incident evidence. | Reliability, observability correlation, SLO validation, monitoring. |
| 12 | **Data engineer** | Silent data quality failures and pipeline regressions. | Trustworthy data pipelines and reconciliation. | Validate pipelines → check quality dimensions → investigate drift. | Data quality, pipelines, reconciliation, schema/migration testing. |
| 13 | **Mobile engineer** | Device/OS fragmentation, mobile performance, lifecycle behavior. | Release confidence for mobile experiences. | Build → device matrix validation → performance/lifecycle checks. | Mobile engine, mobile performance, device compatibility. |
| 14 | **Desktop engineer** | Installer, upgrade, OS integration, Electron/webview issues. | Reliable desktop releases. | Install/upgrade test → OS integration → regression. | Desktop engine, install/upgrade/uninstall testing. |
| 15 | **AI / ML engineer** | Model quality, drift, bias, and regression. | Defensible evaluation of models before release. | Dataset → evaluation run → metric comparison → gate. | AI evaluation engine, ML metrics, drift/bias/regression checks. |
| 16 | **LLM / agent engineer** | Prompt regressions, hallucinations, tool misuse, cost blowups. | Reliable, safe, grounded LLM and agent behavior. | Scenario suite → repeated runs → trajectory and grounding evaluation. | LLM testing, RAG testing, agent trajectory testing, AI safety, AI reliability. |
| 17 | **Engineering manager** | Visibility into quality trends and team risk. | Understand quality trajectory and where to invest. | Review dashboards → inspect regressions → allocate work. | Dashboards, trends, quality model, reporting. |
| 18 | **QA leader** | Test strategy, coverage, and release confidence at scale. | Evidence-based quality governance. | Define policy → review coverage/risk → decide releases. | Quality model, release readiness, test management, reporting, policies. |
| 19 | **Security leader** | Assurance that security validation is controlled and auditable. | Defensible security posture evidence. | Review scope authorization → review findings → audit trail. | Authorization model, auditability, security reporting, compliance evidence. |
| 20 | **Release manager** | Release decisions under time pressure with incomplete information. | Defensible go / conditional / no-go decisions. | Release candidate → quality gates → verdict → record decision. | Release readiness, quality gates, evidence, release history. |
| 21 | **Solo builder / small team** | No QA function; needs automated breadth without a platform team. | Broad automatic coverage with minimal setup. | Onboard target → automatic discovery → recommended testing → findings. | Universal target test journey, autonomous recommendation, default safe profiles. |
| 22 | **Enterprise organization** | Many teams, environments, policies, compliance obligations. | Governed, scalable, auditable quality platform. | Central policy → delegated execution → federated reporting. | Multi-project governance, RBAC, audit, isolation, integrations, compliance evidence. |

### 9.2 Persona design rules

> `WTE-PRD-CORE-004` — WTE must support a **progressive-disclosure** experience: a new user can achieve value with a target and an authorization, while advanced users can control capabilities, engines, policies, and evidence in depth.

> `WTE-PRD-CORE-005` — WTE must not require expert configuration to produce safe, useful first results, and must never produce unsafe first results by default.

> `WTE-PRD-CORE-006` — WTE must support shared organizational workflows (projects, roles, policies, approvals) without making individual usage dependent on organizational setup.

---

## 10. User Problems

These are the concrete problems the product must solve, expressed from the user's perspective. Each maps to capabilities defined later in this document.

### 10.1 Discovery and understanding

- "I don't know everything my application exposes — routes, APIs, third parties, hidden flows."
- "I don't know which parts of the system depend on which others."
- "Each new team member relearns the system from scratch; the knowledge is never captured."
- "I cannot tell what a change will affect."

### 10.2 Test planning and selection

- "I don't know which tests are relevant to this change."
- "Running the full suite takes too long and mostly tests things that did not change."
- "Nobody knows which tests are actually valuable anymore."
- "Critical journeys are less covered than trivial pages."

### 10.3 Execution and reliability

- "Tests fail for environmental reasons; I can't tell signal from noise."
- "Flaky tests waste hours and erode trust in the suite."
- "Fixing selectors consumes more time than finding bugs."
- "I can't run the same validation reliably in local, CI, and staging."

### 10.4 Evidence and diagnosis

- "When something fails, the evidence is spread across five systems."
- "I have to reproduce the failure just to understand what happened."
- "The same underlying bug generates dozens of separate tickets."
- "I can't prove what the failure was after the logs rotate."

### 10.5 Quality and release

- "I can't answer 'is this release ready?' with anything better than 'the pipeline was green'."
- "Quality scores from tools are opaque; nobody knows what they mean."
- "Accessibility, performance, and security regressions are found after release."
- "There is no baseline, so nobody knows whether quality improved or degraded."

### 10.6 Safety and governance

- "I want automated testing to be powerful, but I need to be sure it can't do damage."
- "I can't let an agent browse freely if it might follow instructions embedded in a website."
- "I need an audit trail of exactly what ran, where, and under whose authority."
- "I need to prove that testing never touched production data it shouldn't have."

### 10.7 Breadth and evolution

- "I have tools for ten domains and no shared vocabulary between them."
- "When we adopt a new tool, all our accumulated knowledge becomes obsolete."
- "We need to add Kubernetes, mobile, and AI testing without replatforming."

> `WTE-PRD-CORE-007` — Every capability described in §13 must be traceable to at least one user problem in this section. Capabilities with no user problem must not be prioritized.

---

## 11. Supported Target Universe

### 11.1 Scope statement

WTE's target model must be able to represent essentially any software system its users may operate, under authorization. The list below defines the **long-term target universe**. It does not claim that all target types are testable today — none are.

### 11.2 Target universe by class

| Class | Targets |
|---|---|
| **Web** | Websites, web applications, marketing sites, admin panels, SPAs, SSR/SSG apps, PWAs. |
| **Frontend applications** | Browser-based applications across frameworks and rendering models. |
| **Backend applications** | Server applications, services, monoliths, modular monoliths, background workers. |
| **APIs** | REST, HTTP, GraphQL, gRPC, SOAP/XML, WebSockets, SSE, WebRTC signaling, webhook endpoints. |
| **Microservices & distributed systems** | Service meshes, event-driven architectures, multi-service workflows, consensus systems. |
| **Databases** | Relational, document, key-value, search, time-series, graph, analytical stores. |
| **Data pipelines & analytics** | ETL/ELT, batch and streaming transforms, warehouses, lakehouses, BI layers. |
| **Cloud infrastructure** | AWS, Azure, GCP, and equivalent providers; managed services; identity, networking, storage, compute. |
| **Containers & orchestration** | Container images, runtimes, Kubernetes, and equivalent schedulers. |
| **Infrastructure as code** | Terraform, OpenTofu, CloudFormation, Ansible, and declarative equivalents. |
| **Networks** | DNS, TLS, HTTP delivery, proxies, CDNs, edge platforms, network behavior. |
| **Mobile** | Android, iOS, native, hybrid, webview-based, mobile browsers. |
| **Desktop** | Windows, macOS, Linux, Electron, and native desktop applications. |
| **Enterprise systems** | CRM, ERP, HRIS, identity systems, middleware, document systems, internal services. |
| **CI/CD systems** | Pipelines, builds, artifacts, gates, promotions, rollbacks. |
| **AI systems** | ML models, classifiers, recommenders, computer vision, speech, LLM applications, RAG systems, agents. |
| **IoT & embedded** | Devices, firmware, device-cloud communication, telemetry. *(EXTENSION)* |
| **Realtime & streaming** | Streaming platforms, live media, communication systems. |
| **Safety-critical systems** | Automotive, medical, industrial, aviation, robotics. *(EXTENSION)* |
| **Other software systems** | Any authorized system representable through the platform's target and capability models. |

> `WTE-PRD-TARGET-001` — The target model must represent any authorized software system without requiring the core platform to be redesigned per system class.

> `WTE-PRD-TARGET-002` — Target types not yet supported must be explicitly marked unsupported rather than silently failing or producing fabricated results.

### 11.3 Environment scope

Every target is assessed in the context of one or more environments: local, private/LAN, development, test, staging/pre-production, and production. Environment identity, configuration, and authorization are first-class target attributes (§13.3).

> `WTE-PRD-TARGET-003` — WTE must always know and record which environment an operation ran against, and must never infer production safety from a target being reachable.

---

## 12. Core User Journeys

These journeys define the primary product experiences. Each must be realizable end to end; each stage below is a product requirement area referenced elsewhere in this document.

### 12.1 Universal Target Test

Turn an authorized target into a quality result without the user defining everything manually.

```
Target (URL / endpoint / repository / system descriptor)
   → Authorization (scope, environment, risk class)
   → Discovery (surfaces, routes, APIs, assets, technologies)
   → Application understanding (structure, dependencies, workflows)
   → Recommended testing (capability plan with rationale)
   → Approval or policy-based auto-approval (by risk class)
   → Execution
   → Evidence
   → Findings
   → Quality result (per dimension + overall, explainable)
```

Requirements: `WTE-PRD-DISC-*`, `WTE-PRD-KNOW-*`, `WTE-PRD-GEN-*`, `WTE-PRD-ORCH-*`, `WTE-PRD-EVID-*`, `WTE-PRD-FIND-*`, `WTE-PRD-QUAL-*`.

### 12.2 Developer Change Validation

Validate a change quickly and precisely.

```
Code change (commit / branch / diff)
   → Impact analysis (files, services, routes, APIs, components, workflows)
   → Relevant test selection (risk, history, coverage, flakiness, cost)
   → Execution (local or CI)
   → Comparison with baseline
   → Regression diagnosis (correlated evidence)
   → Result (fixed / broken / flaky / inconclusive)
```

Requirements: `WTE-PRD-IMPACT-*`, `WTE-PRD-SELECT-*`, `WTE-PRD-FLAKY-*`, `WTE-PRD-RCA-*`.

### 12.3 Release Validation

Turn a release candidate into a defensible verdict.

```
Release candidate
   → Required quality gates (policy-driven per release class)
   → Testing (selected + mandated capabilities)
   → Correlation and deduplication
   → Risk assessment (severity × breadth × confidence × history)
   → Verdict: READY / CONDITIONALLY READY / NOT READY
   → Explanation (what passed, what failed, what blocked, what was waived, by whom)
   → Recorded release history
```

Requirements: `WTE-PRD-REL-*`, `WTE-PRD-QUAL-*`, `WTE-PRD-REPORT-*`.

### 12.4 Failure Investigation

Turn a known failure into a probable cause.

```
Known failure (from a run, a report, an alert, or a user report)
   → Reproduce (deterministic replay where possible)
   → Gather evidence (browser, network, API, logs, metrics, traces, database, change history)
   → Correlate across engines and time
   → Determine probable root cause with confidence
   → Identify affected components and workflows
   → Recommend the next action
```

Requirements: `WTE-PRD-CORR-*`, `WTE-PRD-RCA-*`, `WTE-PRD-EVID-*`.

### 12.5 CI/CD Integration

Make WTE a well-behaved participant in delivery pipelines.

```
Pipeline stage
   → WTE (target, scope, policy, change context)
   → Intelligent selection + parallel execution
   → Evidence and findings
   → Quality gate result (pass / warn / block, with explanation)
   → Artifacts (machine-readable results + human summary)
   → Promotion or rollback decision support
```

Requirements: `WTE-PRD-CICD-*`, `WTE-PRD-SELECT-*`, `WTE-PRD-REL-*`, `WTE-PRD-INTEG-*`.

### 12.6 Continuous Testing

Detect meaningful change without human initiation.

```
Scheduled / triggered run
   → Compare against history and baselines
   → Identify meaningful changes only (new, resolved, reopened, regressed, degraded)
   → Suppress known/accepted noise
   → Notify the right audience with evidence
   → Feed back into risk models and test selection
```

Requirements: `WTE-PRD-HIST-*`, `WTE-PRD-FLAKY-*`, `WTE-PRD-OBS-*`, `WTE-PRD-INTEG-*`.

### 12.7 Exploratory / Agentic Investigation

Let the platform investigate an authorized system or a declared goal.

```
Goal (e.g. "validate the checkout journey" / "investigate why dashboard is slow")
   → Plan (bounded, risk-classified, permission-checked)
   → Execute steps with evidence capture
   → Adapt based on observations (within authorization and budget)
   → Produce findings, confidence, and the evidence trail
   → Human-reviewable summary of what was done and why
```

Requirements: `WTE-PRD-AI-*`, `WTE-PRD-AUTH-*`, `WTE-PRD-EVID-*`, `WTE-PRD-FIND-*`.

> `WTE-PRD-CORE-008` — Every journey must be resumable and inspectable: a user must be able to see what ran, what was observed, what was concluded, and why, at every stage.

---

## 13. Universal Testing Capability Model

### 13.1 Conceptual hierarchy

The platform distinguishes five layers. Confusing them is a design defect (`P6`).

```
TESTING DOMAIN
      ↓
TESTING CATEGORY
      ↓
CAPABILITY
      ↓
ENGINE / ADAPTER
      ↓
TOOL / FRAMEWORK / SERVICE
```

Definitions:

| Layer | Meaning | Example |
|---|---|---|
| **Testing domain** | A broad area of quality risk that the platform understands. | Accessibility Testing |
| **Testing category** | A coherent group of testing activities inside a domain. | Automated accessibility scanning |
| **Capability** | A product-level operation WTE can plan, authorize, execute, and evaluate. Vendor-independent. | `accessibility.scan` |
| **Engine / adapter** | A platform component that implements one or more capabilities, possibly by wrapping a tool. | axe adapter |
| **Tool** | An external or internal implementation artifact. Replaceable. | axe-core |

Additional examples:

```
Load Testing
      ↓
HTTP load generation
      ↓
load.execute
      ↓
k6 adapter
      ↓
k6
```

```
Browser Automation
      ↓
Page navigation
      ↓
browser.navigate
      ↓
Playwright adapter
      ↓
Playwright
```

> `WTE-PRD-CORE-009` — Product requirements are defined at the **domain, category, and capability** layers. WTE must never hard-code a requirement at the tool layer.

> `WTE-PRD-CORE-010` — Every capability must declare: its capabilities identifier, the risk class it belongs to, the environments it may run in, the evidence it produces, and the evaluators that judge its observations.

### 13.2 How to read §13

§13 defines the **long-term capability model**: what WTE must eventually be able to represent, plan, authorize, execute, evaluate, and report. It is not an implementation plan.

Reading rules:

1. **Nothing here is implemented today** (§1.3).
2. **Taxonomy ≠ engines** (§8, `NG-11`). Many categories are served by a small number of engines; engine composition is defined in `ARCHITECTURE.md`.
3. Each subsection states its **horizon** and its **authorization sensitivity**.
4. **Authorization sensitivity** uses the risk classes defined in §27: `READ_ONLY`, `SAFE_ACTIVE`, `MUTATING`, `LOAD_GENERATING`, `SECURITY_ACTIVE`, `INFRASTRUCTURE_MUTATING`, `DESTRUCTIVE`.
5. Capability identifiers are **product vocabulary**, not vendor bindings. They form the basis of the capability registry (§18).

---

### 13.3 Testing Foundations

**Horizon:** FOUNDATIONAL
**Authorization:** mixed — mostly `READ_ONLY` and `SAFE_ACTIVE`

Testing foundations are the conceptual testing disciplines the platform must be able to represent, plan, and reason about. They are not capabilities in themselves; they are the vocabulary the planning layer uses to describe *how* something should be tested.

#### 13.3.1 Testing approaches

| Discipline group | What WTE must represent |
|---|---|
| Access to internals | Static testing, dynamic testing. |
| Knowledge of internals | Black-box, white-box, gray-box testing. |
| Basis of design | Specification-based, structure-based, experience-based testing. |
| Degree of automation | Manual, automated, exploratory, hybrid. |
| Intent | Positive testing, negative testing. |
| Driving factor | Risk-based testing, change-based testing. |
| Derivation method | Model-based, property-based, metamorphic, differential testing. |
| Test design techniques | Boundary value analysis, equivalence partitioning, decision tables, state transition testing, pairwise/combinatorial testing. |

> `WTE-PRD-CORE-011` — WTE must be able to classify any planned or executed test by its foundations (access, knowledge, basis, automation, intent, driver, derivation) so that coverage and gaps can be reasoned about in testing-theory terms.

> `WTE-PRD-CORE-012` — WTE must support test design techniques as planning primitives (generate boundary cases, equivalence classes, decision tables, state transitions, combinatorial sets) wherever the application model provides enough structure.

> `WTE-PRD-CORE-013` — WTE must distinguish manual testing, automated testing, and exploratory testing in the model, and must support recording manual and exploratory results into the same evidence and finding models.

#### 13.3.2 Release and change testing

| Category | Representative capabilities |
|---|---|
| Pre-merge / pre-build | Smoke testing, sanity testing. |
| Change validation | Regression testing, selective regression, confirmation/retesting. |
| Release validation | Release testing, smoke validation of a release candidate. |
| Post-deployment | Production verification, canary validation, post-deployment validation. |

> `WTE-PRD-CORE-014` — WTE must support release-oriented test categories as first-class plans with policy association (which gates require which categories for which release classes).

> `WTE-PRD-CORE-015` — WTE must support **selective regression**: determining, with explainable rationale, which regression tests are relevant to a given change set.

---

### 13.4 Test Levels

**Horizon:** FOUNDATIONAL (unit, integration, system, E2E, acceptance); PLANNED (operational acceptance, alpha/beta/field)

The platform must understand where a test sits in the verification stack:

```
Unit → Component → Integration → System → End-to-End → Acceptance
                                                        ├── User Acceptance
                                                        ├── Operational Acceptance
                                                        └── Alpha / Beta / Field
```

| Level | What WTE must represent |
|---|---|
| **Unit testing** | Verification of individual units; consumption of results from code-level frameworks. |
| **Component testing** | Verification of a component or module in isolation. |
| **Integration testing** | Verification of interactions between components, services, or systems. |
| **System testing** | Verification of a complete system against requirements. |
| **End-to-end testing** | Verification of complete user or business flows across the whole stack. |
| **Acceptance testing** | Verification against business acceptance criteria. |
| **User acceptance testing** | Business/user validation, including manual sign-off evidence. |
| **Operational acceptance testing** | Backup, restore, monitoring, failover, operational readiness. |
| **Alpha testing** | Internal pre-release validation. |
| **Beta testing** | External pre-release validation with feedback capture. |
| **Field testing** | Real-world environment validation. |

> `WTE-PRD-CORE-016` — Every test definition must carry a test level, and WTE must be able to report coverage and gaps by level.

> `WTE-PRD-CORE-017` — WTE must integrate with existing unit/component/integration test ecosystems to consume their results rather than requiring migration into WTE.

> `WTE-PRD-CORE-018` — Acceptance, alpha, beta, and field testing must support human-reported results (structured sign-off and feedback) recorded with the same evidence discipline as automated results.

---

### 13.5 Target & Environment Model

**Horizon:** FOUNDATIONAL
**Authorization:** `READ_ONLY` for detection; environment classification gates everything else

The target and environment model is a foundational primitive. Everything WTE does is relative to a target, an environment, a scope, and an authorization.

| Category | What WTE must represent |
|---|---|
| **Target identity** | Name, type, owner, description, system class, version context. |
| **Target type** | Web, API, mobile, desktop, database, pipeline, infrastructure, AI system, etc. |
| **Endpoint surface** | URLs, hostnames, IP ranges, API roots, repositories, clusters, accounts, datasets. |
| **Environment** | localhost, LAN/private, development, test, staging/pre-production, production, custom. |
| **Environment classification** | Which environment is production-like; which may be mutated; which are off-limits. |
| **Environment comparison** | Comparing configuration, behavior, versions, and data shape between environments. |
| **Environment drift** | Detecting divergence between environments that should be equivalent. |
| **Configuration** | Environment variables, feature flags, secrets *references*, service endpoints. |
| **Network configuration** | Proxy configuration, routing, DNS overrides, host mappings, egress rules. |
| **Target validation** | Verifying reachability, identity, and that the target is what it claims to be. |
| **Scope** | Domains, paths, services, accounts, and resources explicitly in and out of scope. |
| **Authorization boundaries** | Which risk classes are authorized, by whom, until when, and under what conditions. |

> `WTE-PRD-TARGET-004` — WTE must require every execution to resolve to exactly one target, one environment, and one effective authorization before any operation begins.

> `WTE-PRD-TARGET-005` — WTE must classify environments and must treat production as a distinct, higher-risk class requiring separate authorization and separate capability policy.

> `WTE-PRD-TARGET-006` — WTE must support scope declarations that include positive scope (allowed) and negative scope (explicitly forbidden), and must enforce both.

> `WTE-PRD-TARGET-007` — WTE must support environment comparison and drift detection between environments declared comparable.

> `WTE-PRD-TARGET-008` — WTE must validate target reachability and identity before discovery or execution, and must fail clearly rather than proceeding on an unverified target.

> `WTE-PRD-TARGET-009` — WTE must enforce SSRF protections and private-network controls so that agent-driven or user-driven requests cannot reach unintended internal resources.

> `WTE-PRD-TARGET-010` — Proxy, DNS, and routing overrides must be explicit, recorded, and scoped to a run; they must never silently apply globally.

---

### 13.6 Discovery & Reconnaissance

**Horizon:** FOUNDATIONAL (web); PLANNED (API, infrastructure, mobile, data, AI)
**Authorization:** `READ_ONLY` by default; intrusive discovery requires `SAFE_ACTIVE` authorization

Discovery is how WTE learns what exists. It is the input to the application knowledge model and to all planning.

| Category group | What WTE must discover |
|---|---|
| **Web surface** | Sites, pages, routes, hidden/unlinked routes, navigation structures, links, redirects. |
| **Interactive elements** | Forms, inputs, buttons, controls, menus, dialogs, file inputs, uploads/downloads. |
| **Assets** | Images, fonts, scripts, stylesheets, media, documents. |
| **Rendering structures** | Frames/iframes, Shadow DOM, Web Components, portals, canvas-rendered UI. |
| **Platform features** | Service workers, PWA manifests, storage usage, caching layers. |
| **APIs** | REST endpoints, GraphQL schemas, webhooks, realtime channels (WebSockets/SSE), gRPC services. |
| **Third parties** | External services called by the application, analytics, trackers, embedded widgets. |
| **Technology stack** | Frameworks, libraries, build artifacts, server signatures, CMS, e-commerce platforms, CDN. |
| **Authentication surfaces** | Login systems, identity providers, token mechanisms, consent/authorization flows. |
| **Non-web surfaces** | Databases, message topics, queues, infrastructure resources, datasets, model endpoints. |

> `WTE-PRD-DISC-001` — Discovery must produce a structured, reviewable inventory of the target's surfaces, and record how each item was discovered.

> `WTE-PRD-DISC-002` — Discovery must be incremental and repeatable: re-running discovery must identify what is new, changed, or disappeared since the previous discovery, and feed that into application knowledge and risk.

> `WTE-PRD-DISC-003` — Discovery must respect scope and authorization, and must never enumerate resources outside declared scope.

> `WTE-PRD-DISC-004` — Discovery must record evidence for discovered facts (the request/response, DOM snapshot, schema document, or source reference that established the fact).

> `WTE-PRD-DISC-005` — Discovery must never fabricate structure: unknown or uncertain elements must be marked uncertain, not guessed.

> `WTE-PRD-DISC-006` — Discovery must be safe by default: read-oriented, rate-limited, and non-destructive unless a higher authorization class explicitly permits more.

---

### 13.7 Application Knowledge

**Horizon:** FOUNDATIONAL (core graph); PLANNED (graph deepening: coverage, changes, releases)
**Authorization:** `READ_ONLY`

Application knowledge is WTE's persistent model of the system under test. It is what turns a set of discovered facts into an understanding that improves every subsequent run.

#### 13.7.1 Entities the model must represent

```
Applications · Pages · Routes · Components · APIs · Services · Workflows · Roles ·
Permissions · Dependencies · Databases · Infrastructure · Third-party services ·
Tests · Coverage · Findings · Changes · Failures · Releases
```

#### 13.7.2 Relationships the model must represent

```
Page        → contains →  Component
Component   → calls    →  API
API         → accesses →  Service
Service     → accesses →  Database
Role        → can access → Route
Workflow    → uses     →  Pages
Workflow    → uses     →  APIs
Test        → covers   →  Workflow
Finding     → affects  →  Component
Change      → affects  →  API
Release     → contains →  Change
```

> `WTE-PRD-KNOW-001` — WTE must maintain a persistent application knowledge model per system, spanning applications, structure, dependencies, workflows, identities, tests, findings, changes, and releases.

> `WTE-PRD-KNOW-002` — Knowledge must be **evidence-backed**: each asserted relationship must be traceable to the discovery, observation, or source artifact that established it.

> `WTE-PRD-KNOW-003` — Knowledge must be **queryable**: users and engines must be able to ask what depends on what, what a change affects, which tests cover a workflow, and which findings affect a component.

> `WTE-PRD-KNOW-004` — Knowledge must be **living**: it evolves from discovery, execution, correlation, and change analysis, and it records when and why it changed.

> `WTE-PRD-KNOW-005` — Knowledge must support **uncertainty**: inferred relationships carry confidence and provenance and are distinguishable from observed ones.

> `WTE-PRD-KNOW-006` — Knowledge must be per-system isolated in multi-tenant deployments; one customer's application knowledge must never leak into another's.

> `WTE-PRD-KNOW-007` — Application knowledge must improve testing: planning, selection, generation, correlation, and root-cause analysis must all consume it.

---

### 13.8 Browser Automation

**Horizon:** FOUNDATIONAL
**Authorization:** `SAFE_ACTIVE` for interaction; `READ_ONLY` for navigation and observation

Browser automation is the foundational execution capability for web and web-based targets.

| Category group | What WTE must support |
|---|---|
| **Lifecycle** | Browser launch, contexts, pages, cleanup, crash recovery. |
| **Navigation** | URLs, history, back/forward, reload, deep links, redirects, waits. |
| **Interaction** | Mouse, keyboard, touch, drag, scroll, hover, focus, text entry, selection. |
| **Forms** | Inputs, validation, multi-step forms, autofill, resets. |
| **Files** | Downloads, uploads, file choosers, drag-and-drop files. |
| **System interactions** | Clipboard, permissions, popups, dialogs, notifications, geolocation, camera, microphone. |
| **Contexts** | Frames/iframes, tabs, windows, browser contexts, storage isolation. |
| **State** | Cookies, localStorage/sessionStorage, IndexedDB, cache, service worker state. |
| **Emulation** | Device emulation, viewport, user agent, network conditions, timezone, locale. |
| **Instrumentation** | Console output, network capture (HAR), traces, screenshots, video, DOM snapshots, accessibility trees. |

> `WTE-PRD-BROWSER-001` — WTE must support browser automation through multiple interchangeable engines; no single browser automation vendor may be a product requirement.

> `WTE-PRD-BROWSER-002` — Browser execution must capture, at minimum: console output, network activity, DOM state at failure, screenshot, and browser trace metadata for every failed step, and must support full-session capture when enabled.

> `WTE-PRD-BROWSER-003` — Browser automation must be deterministic where possible: stable waiting, state-based synchronization, and auto-waiting are required; arbitrary sleeps are prohibited as a primary mechanism.

> `WTE-PRD-BROWSER-004` — WTE must support parallel, isolated browser contexts so executions cannot contaminate each other's state.

> `WTE-PRD-BROWSER-005` — WTE must record browser/engine versions and emulation parameters as execution metadata for reproducibility.

> `WTE-PRD-BROWSER-006` — Browser interactions must respect authorization classes: any interaction that changes server-side state is `MUTATING` and must be authorized accordingly.

---

### 13.9 Functional & Workflow Testing

**Horizon:** FOUNDATIONAL (core functional); PLANNED (business logic, complex workflows)
**Authorization:** mixed — observation `READ_ONLY`, interaction `SAFE_ACTIVE`, state-changing flows `MUTATING`

#### 13.9.1 Functional UI and application behavior

| Category group | What WTE must represent |
|---|---|
| **Navigation & structure** | Navigation, links, menus, tabs, breadcrumbs. |
| **Interaction** | Buttons, forms, validation, keyboard shortcuts. |
| **Data operations** | CRUD flows, search, filtering, sorting, pagination, infinite scroll, tables, data grids. |
| **Content & visualization** | Charts, dashboards, wizards/steppers, modals, drawers. |
| **State & session** | Application state, sessions, refresh behavior, deep links, back/forward, recovery from interruptions. |
| **Feedback** | Notifications, toasts, confirmations, error messages. |
| **Transfers** | File uploads and downloads as functional flows. |

#### 13.9.2 Business logic testing

| Category group | What WTE must represent |
|---|---|
| **Rules** | Business rules, eligibility, entitlements, limits, thresholds. |
| **Money & value** | Pricing, discounts, taxes (logic-level), billing logic, subscription logic. |
| **Process** | Approval workflows, state transitions, workflow invariants. |
| **Inventory & allocation** | Stock rules, availability, reservation logic. |
| **Calculations** | Calculated totals, derived values, rounding, reconciliation of computed outputs. |

#### 13.9.3 User journey & workflow testing

| Category group | What WTE must represent |
|---|---|
| **Critical journeys** | The business-critical paths the organization defines (e.g. signup, checkout, payment, onboarding). |
| **Cross-page workflows** | Multi-page flows with state carried across pages. |
| **Cross-service workflows** | Flows spanning multiple services/systems. |
| **Long-running workflows** | Workflows spanning minutes/hours/days, including async completion. |
| **Failure paths** | Interrupted journeys, partial completion, compensation, rollback, recovery. |

> `WTE-PRD-FUNC-001` — WTE must test functional behavior through the browser and through APIs, and must support the same capability against both surfaces.

> `WTE-PRD-FUNC-002` — WTE must model **workflows** as first-class entities with declared steps, expected outcomes, and criticality, so that workflow results drive risk and release decisions.

> `WTE-PRD-FUNC-003` — WTE must support negative testing and error-path testing as first-class intents, not as incidental variations of happy paths.

> `WTE-PRD-FUNC-004` — WTE must support business rule validation at the level of declared rules and invariants where the system exposes or documents them, and must never invent business rules silently.

> `WTE-PRD-FUNC-005` — WTE must test workflow recovery: interruption, partial completion, retry, compensation, and resumption behavior.

> `WTE-PRD-FUNC-006` — WTE must distinguish failures of the workflow under test from failures of the test itself (test defect), and must report each accordingly.

> `WTE-PRD-FUNC-007` — Functional results must feed application knowledge (which workflows use which pages and APIs) and history (workflow pass/fail over time).

---

### 13.10 UI Testing

**Horizon:** PLANNED (observation-based UI checks); LONG-TERM (full UI rule library)
**Authorization:** `READ_ONLY` (observation); `SAFE_ACTIVE` (interaction-state triggering)

| Category group | What WTE must observe and evaluate |
|---|---|
| **Rendering** | Components render, layout composition, structural presence. |
| **Interaction states** | Hover, focus, active, disabled, selected, loading, empty, error. |
| **Layout** | Alignment, spacing, grid consistency, margins, padding, ordering. |
| **Typography** | Font family, size, weight, line height, truncation, wrapping. |
| **Color** | Foreground/background application, contrast inputs, theme consistency. |
| **Visual layers** | Z-index conflicts, overlays, occlusion, clipping, overflow. |
| **Media** | Icons, images, aspect ratios, broken media. |
| **Responsive states** | See §13.13. |
| **Stability** | Layout shifts, flicker, content jumping. |

> `WTE-PRD-UIUX-001` — UI testing must separate **observation** (measured properties of the rendered interface) from **evaluation** (rules that judge those properties), and must store both.

> `WTE-PRD-UIUX-002` — WTE must extract UI observations as structured, machine-readable facts (element identity, geometry, computed style, state) in addition to any screenshot.

> `WTE-PRD-UIUX-003` — WTE must evaluate UI quality against configurable, versioned rule sets, and must explain which rule produced which finding.

> `WTE-PRD-UIUX-004` — UI evaluation must be tolerant of legitimate design variance: thresholds, exception lists, and per-project rule configuration are required.

---

### 13.11 UX Testing

**Horizon:** LONG-TERM (observation-based signals PLANNED; evaluation LONG-TERM)
**Authorization:** `READ_ONLY` / `SAFE_ACTIVE`

UX testing spans objective observation and subjective evaluation, and WTE must keep these strictly separate.

| Layer | What WTE must support |
|---|---|
| **Objective observation** | Interaction friction signals (excess steps, repeated retries, dead ends), missing feedback after actions, inconsistent affordances, focus/navigation order, task completion paths, state visibility (loading/empty/error), readability metrics (text size, contrast, density), touch target sizes, information hierarchy (heading structure, landmarks). |
| **Subjective evaluation** | Usability heuristics, discoverability, clarity, cognitive load, consistency, error prevention/recovery, navigation clarity, ergonomics — evaluated through explicit criteria, user research inputs, or human review workflows. |

> `WTE-PRD-UIUX-005` — WTE must never present subjective UX judgments as objective measurements. Subjective evaluations must be labeled as evaluations, carry their criteria and confidence, and never be merged into objective evidence.

> `WTE-PRD-UIUX-006` — WTE must support human-in-the-loop UX evaluation: recording expert or user assessments against the same finding and evidence models used by automated checks.

> `WTE-PRD-UIUX-007` — WTE must convert recurring UX observations (e.g. repeated failure to reach a goal, dead-end navigation, missing action feedback) into findings with evidence, without claiming to measure user satisfaction.

> `WTE-PRD-UIUX-008` — WTE must be capable of considering UX findings in quality scoring as a separate dimension with explicit policy, never silently folded into functional scoring.

---

### 13.12 Visual Testing

**Horizon:** PLANNED
**Authorization:** `READ_ONLY`

| Category group | What WTE must support |
|---|---|
| **Capture** | Page screenshots, viewport screenshots, element screenshots, full-page capture, state-specific capture. |
| **Comparison** | Pixel comparison, structural comparison, semantic comparison. |
| **Baselines** | Baseline creation, approval, versioning, promotion between environments, history of baseline changes. |
| **Regression** | Visual regression detection, per-component and per-page, responsive variants, cross-browser variants, theme variants. |
| **Anomaly detection** | Detection of visual anomalies beyond strict pixel diffing (layout breakage, overlap, missing elements, clipping). |
| **Noise control** | Masking, dynamic content handling, anti-aliasing tolerance, threshold management to prevent false positives. |

> `WTE-PRD-VISUAL-001` — Visual testing must support explicit baseline management: baselines are approved artifacts with owners, history, and rationale — never silently overwritten.

> `WTE-PRD-VISUAL-002` — Visual comparison must produce both a verdict and the artifacts that justify it (before/after/diff), stored as evidence.

> `WTE-PRD-VISUAL-003` — Visual testing must minimize false positives through deterministic capture conditions (viewport, device pixel ratio, fonts, animations disabled, timestamps masked) recorded as evidence metadata.

> `WTE-PRD-VISUAL-004` — WTE must distinguish intentional visual change (design change, content change) from regression, and must support workflows for reviewing and accepting visual changes.

> `WTE-PRD-VISUAL-005` — Visual findings must be linked to the components and routes they affect in the application knowledge model.

---

### 13.13 Accessibility

**Horizon:** PLANNED (deterministic scanning); LONG-TERM (assistive technology validation, full WCAG workflow assessment)
**Authorization:** `READ_ONLY` / `SAFE_ACTIVE`

| Category group | What WTE must support |
|---|---|
| **Standards** | WCAG conformance at A / AA / AAA targets (as declared), success-criteria mapping. |
| **Semantics** | Semantic HTML, landmarks, headings, lists, tables, form labeling. |
| **ARIA** | Roles, states, properties, accessible names and descriptions, ARIA correctness (valid, supported, non-conflicting). |
| **Keyboard** | Full keyboard operability, focus order, focus visibility, focus trapping, skip links, keyboard traps. |
| **Visual accessibility** | Contrast ratios (text, large text, non-text), text scaling, reflow, motion/animation preferences, target sizes. |
| **Structure** | Page language, titles, document structure, reading order. |
| **Dynamic content** | Live regions, notifications, focus management in modals/dialogs/SPA navigation. |
| **Assistive technology validation** | Accessibility tree analysis, screen reader behavior validation, manual/assisted review workflows. |

> `WTE-PRD-A11Y-001` — Accessibility testing must be primarily evidence-based and deterministic: computed roles, names, states, contrast, geometry, and focus behavior — not opinion.

> `WTE-PRD-A11Y-002` — WTE must map findings to specific WCAG success criteria and severity levels, and must state the target conformance level the result refers to.

> `WTE-PRD-A11Y-003` — WTE must support automated scanning, assisted/manual validation, and assistive-technology-oriented checks as separate, honestly labeled categories of evidence.

> `WTE-PRD-A11Y-004` — WTE must never claim full accessibility conformance from automated scanning alone, and must state what portion of criteria automated checks can cover.

> `WTE-PRD-A11Y-005` — Accessibility coverage must be reported at the level of pages, components, and workflows, with gaps identified rather than hidden.

> `WTE-PRD-A11Y-006` — Accessibility results must be tracked historically so that regressions (a previously passing criterion now failing) are detected.

---

### 13.14 Responsive & Compatibility Testing

**Horizon:** PLANNED
**Authorization:** `READ_ONLY`

| Category group | What WTE must support |
|---|---|
| **Viewports** | Desktop, laptop, tablet, mobile, foldable; portrait and landscape; custom viewports; device pixel ratios. |
| **Breakpoints** | Verification at and around declared breakpoints, including boundary conditions. |
| **Layout behavior** | Overflow, collision, clipping, text truncation, scroll behavior, adaptive navigation (menus → hamburger → sheets). |
| **Media behavior** | Responsive images, responsive typography, media loading by viewport. |
| **Touch** | Touch target sizing and spacing, gesture support. |
| **Browsers** | Chromium/Chrome, Edge, Firefox, Safari/WebKit, and mobile browser equivalents. |
| **Runtime compatibility** | Version matrices for browsers, operating systems, devices, runtimes. |
| **Component compatibility** | Database versions, API versions, dependency versions, protocol versions. |
| **Directionality** | Backward compatibility, forward compatibility, interoperability, conformance. |

> `WTE-PRD-COMPAT-001` — WTE must support a declared **compatibility matrix** per target (which browsers, versions, viewports, OSes, runtimes must be supported) and report results against it.

> `WTE-PRD-COMPAT-002` — Responsive testing must be able to detect layout defects objectively (overflow, overlap, clipping, off-screen elements, unreadable text sizes), not merely capture screenshots.

> `WTE-PRD-COMPAT-003` — Compatibility findings must identify the exact combination (browser/version/viewport/OS) where the defect occurs, and whether it is unique to that combination or general.

> `WTE-PRD-COMPAT-004` — WTE must support versioned compatibility policies so that dropping or adding support is an explicit, reviewable decision.

---

### 13.15 API & Protocol Testing

**Horizon:** PLANNED (REST/HTTP foundation); LONG-TERM (full protocol range)
**Authorization:** `SAFE_ACTIVE` (read calls); `MUTATING` (write calls)

#### 13.15.1 REST / HTTP

| Category group | What WTE must support |
|---|---|
| **Request construction** | Methods, headers, cookies, query and path parameters, bodies (JSON, form, multipart, binary). |
| **Authentication** | Auth flows in requests, token handling, credential references. |
| **Validation** | Status codes, headers, body shape, schema conformance, content types. |
| **Semantics** | Idempotency, pagination, filtering, sorting, rate limits, retries, caching headers. |
| **Errors** | Error responses, error codes, error message quality, failure modes. |
| **Versioning & compatibility** | API version behavior, backward/forward compatibility. |

#### 13.15.2 GraphQL

Queries, mutations, subscriptions, schema introspection, variables, fragments, pagination patterns, authorization enforcement per field, query complexity/depth limits, and error semantics.

#### 13.15.3 gRPC

Unary calls, streaming (client, server, bidirectional), protobuf message validation, metadata, authentication, status codes, interoperability, and backward compatibility of service contracts.

#### 13.15.4 SOAP / XML

WSDL consumption, SOAP envelope construction, XML schema validation, WS-Security, authentication, fault handling, and interoperability.

#### 13.15.5 Realtime protocols

WebSockets, Server-Sent Events, WebRTC signaling and media paths, streaming semantics: connection lifecycle, reconnection behavior, message ordering, duplicate delivery, latency behavior, authorization on channels, backpressure, and partial-failure behavior.

#### 13.15.6 Messaging & event systems

Kafka, RabbitMQ/AMQP, MQTT, NATS, Redis Streams, cloud queues/topics (SQS, SNS, Pub/Sub, Service Bus), and equivalents: producers, consumers, schemas, ordering, delivery guarantees, retries, dead-letter queues, and eventual consistency behavior.

#### 13.15.7 Contract & schema testing

Provider/consumer contracts, consumer-driven contracts, OpenAPI documents, JSON Schema, GraphQL schemas, XML schemas, protobuf definitions, database schemas: validation, compatibility checking, and **breaking-change detection** across versions.

#### 13.15.8 Mocking & service virtualization

Mocks, stubs, fakes, service virtualization, dependency simulation, fault simulation, and deterministic integration environments — so that integration and API testing can run repeatably when real dependencies are unavailable, expensive, unstable, or unsafe to use.

> `WTE-PRD-API-001` — WTE must test APIs as first-class targets, independent of any UI, and must support the same capability against HTTP, GraphQL, gRPC, SOAP, and realtime protocols.

> `WTE-PRD-API-002` — WTE must detect and report breaking contract changes with the specific incompatibility identified, and must distinguish breaking from non-breaking changes.

> `WTE-PRD-API-003` — API testing must support schema-driven validation and generation of valid, boundary, and invalid inputs.

> `WTE-PRD-API-004` — WTE must support event- and message-based testing, including asynchronous verification (waiting for eventual outcomes) with bounded, declared timeouts.

> `WTE-PRD-API-005` — API calls that mutate state must be classified as `MUTATING` and must require appropriate authorization and environment permission.

> `WTE-PRD-API-006` — WTE must support mocking and service virtualization (§13.15.8) so that API and integration testing can run deterministically without unavailable dependencies.

---

### 13.16 Authentication, Authorization & Session Testing

**Horizon:** PLANNED (authentication basics); LONG-TERM (full identity lifecycle, advanced authorization models)
**Authorization:** `SAFE_ACTIVE`; identity-lifecycle mutations are `MUTATING`

#### 13.16.1 Authentication

Login, logout, registration, password reset, password change, email verification, OTP (email/SMS), TOTP, MFA, passkeys/WebAuthn, SSO, OAuth, OIDC, SAML, LDAP, Active Directory, social login, magic links, remember-me, device trust, token refresh, token rotation.

#### 13.16.2 Authorization & identity

RBAC, ABAC, ReBAC, PBAC, object-level authorization, function-level authorization, field-level authorization, row-level authorization, tenant isolation, permission inheritance, explicit deny, privilege escalation resistance, direct-route authorization (deep-link access without UI affordances), API authorization parity with UI authorization, identity provisioning and deprovisioning, identity lifecycle.

#### 13.16.3 Session security

Session creation, expiry, fixation resistance, logout invalidation, token expiry, token rotation, cookie protection attributes, concurrent session behavior, device session management.

> `WTE-PRD-IDENT-001` — WTE must support testing authenticated experiences across common identity mechanisms without requiring the user to disable security controls.

> `WTE-PRD-IDENT-002` — WTE must test authorization as a matrix: roles × functions × objects × tenants, and must report both over-permission and under-permission findings.

> `WTE-PRD-IDENT-003` — WTE must explicitly test **authorization parity** between UI affordances and direct API/route access, since UI-only enforcement is a defect class.

> `WTE-PRD-IDENT-004` — WTE must test tenant isolation as a first-class requirement for multi-tenant systems.

> `WTE-PRD-IDENT-005` — WTE must test session lifecycle: expiration, invalidation on logout, rotation, concurrent sessions, and behavior after credential change.

> `WTE-PRD-IDENT-006` — Credentials and tokens used for testing must be referenced through the secret model (§27.6), never embedded in test definitions, logs, evidence, or reports.

---

### 13.17 Security Testing

**Horizon:** PLANNED (passive/configuration checks); LONG-TERM (`SECURITY_ACTIVE` validation)
**Authorization:** `SECURITY_ACTIVE` required for any active testing; `READ_ONLY` for passive analysis

Security testing in WTE is authorization-gated, scope-bound, and evidence-producing.

#### 13.17.1 Security testing categories

| Category group | What WTE must support |
|---|---|
| **Information gathering** | Passive reconnaissance within scope: exposed metadata, technology fingerprinting, published artifacts. |
| **Configuration** | Security headers, cookie attributes, TLS configuration, CORS policies, exposed debug/admin surfaces (detection only). |
| **Identity** | Registration, enumeration resistance, account lifecycle behavior. |
| **Authentication** | Authentication strength, lockout behavior, MFA enforcement, credential handling. |
| **Authorization** | Access control validation per §13.16. |
| **Session** | Session handling, fixation, invalidation, token handling. |
| **Input validation** | Input handling, encoding, output escaping — validated through safe, controlled probes. |
| **Injection** | Injection-class defects (SQL/NoSQL/command/template/LDAP/header) validated safely and only under `SECURITY_ACTIVE` authorization, with strict blast-radius limits. |
| **Cryptography** | Cryptographic configuration, algorithm strength, key handling expectations. |
| **Business logic security** | Abuse of workflows: replay, race, parameter tampering, workflow bypass, quantity/price manipulation. |
| **Client-side security** | DOM-based issues, client-side trust assumptions, sensitive data exposure in client assets. |
| **API security** | API-specific authorization, mass assignment, rate limiting, excessive data exposure. |
| **HTTP security** | Header policy, transport security, caching of sensitive responses (see §13.19). |
| **Threat validation** | Validating that declared threats and abuse cases are actually mitigated. |
| **Abuse cases** | Test scenarios representing realistic misuse, fraud, and hostile workflows. |

#### 13.17.2 Application security technologies

SAST, DAST, IAST, RASP validation, software composition analysis (SCA), dependency vulnerability analysis, secret scanning, SBOM generation and verification, supply-chain security, fuzzing, penetration-testing support, and security regression testing.

> `WTE-PRD-SEC-001` — No security testing may execute without an `AUTHORIZATION: SECURITY_ACTIVE` grant that names scope, targets, risk class, time window, and responsible party.

> `WTE-PRD-SEC-002` — WTE must prioritize passive and configuration-based security evidence as the default, and must require explicit escalation for active probing.

> `WTE-PRD-SEC-003` — WTE must never exploit a discovered vulnerability beyond the minimum needed to establish evidence, and must never exfiltrate real data.

> `WTE-PRD-SEC-004` — Security findings must include severity, exploitability context, affected component, supporting evidence, and remediation guidance, and must be reported through the standard finding model.

> `WTE-PRD-SEC-005` — WTE must support security regression: verifying that a previously fixed vulnerability class no longer reproduces.

> `WTE-PRD-SEC-006` — WTE must produce machine-readable security outputs (e.g. SARIF-class formats) for integration into security tooling, subject to the reporting requirements in §30.

> `WTE-PRD-SEC-007` — WTE must enforce rate limits, concurrency limits, and blast-radius controls on all active security testing so that a test cannot degrade the target.

> `WTE-PRD-SEC-008` — Security testing must be fully auditable: who authorized what, against which scope, when, with which engine, and with what result.

---

### 13.18 Cryptography, TLS & HTTP Security

**Horizon:** PLANNED
**Authorization:** `READ_ONLY`

#### 13.18.1 Cryptography & TLS

Certificates, chains, expiry, hostname/SAN validation, TLS versions, cipher suites, HSTS, OCSP/stapling, key handling expectations, randomness assumptions, and cryptographic configuration review.

#### 13.18.2 HTTP security

Content Security Policy (presence, correctness, effective enforcement), CORS policy correctness (including permissive wildcards and credential combinations), HSTS, clickjacking protection, Referrer-Policy, Permissions-Policy, mixed content, caching of sensitive responses, cookie attributes (Secure, HttpOnly, SameSite, Path, Domain, prefix rules), and security headers generally.

> `WTE-PRD-NET-001` — WTE must validate TLS configuration and certificate health for authorized targets, including expiry monitoring and chain validation.

> `WTE-PRD-NET-002` — WTE must evaluate HTTP security policies as declared expectations (policy-as-rule) and report deviations with evidence of the actual headers observed.

> `WTE-PRD-NET-003` — Cryptographic and HTTP-security findings must be severity-classified and tracked historically, so regressions in security posture are detectable.

---

### 13.19 Privacy

**Horizon:** LONG-TERM
**Authorization:** `READ_ONLY` (observation); `SAFE_ACTIVE` (interaction with consent flows)

| Category group | What WTE must support |
|---|---|
| **Consent** | Consent mechanisms presence, granularity, blocking-before-consent behavior, withdrawal flows. |
| **Cookies & tracking** | Cookie inventory, classification, third-party trackers, tracking behavior before/after consent. |
| **Data leakage** | Detection of PII in client-side assets, responses, URLs, logs, and error surfaces. |
| **Data lifecycle** | Data minimization signals, retention indicators, deletion/export flow verification. |
| **Privacy controls** | User-facing privacy controls behavior (opt-out, deletion request, data export). |
| **Sensitive evidence** | Handling of evidence that may itself contain personal data. |

> `WTE-PRD-PRIV-001` — WTE must produce **technical compliance evidence** (observable behavior, configurations, artifacts) and must never automatically assert legal compliance.

> `WTE-PRD-PRIV-002` — WTE must classify evidence containing personal or sensitive data and apply the configured retention, access, and redaction policy to it.

> `WTE-PRD-PRIV-003` — WTE must support redaction of sensitive data in evidence and reports, with redaction recorded as an audit event rather than a silent modification.

> `WTE-PRD-PRIV-004` — WTE must support data minimization in its own operation: collecting the minimum evidence necessary for the configured purpose.

---

### 13.20 Performance Testing

**Horizon:** PLANNED (frontend/page performance); LONG-TERM (backend, runtime, resource)
**Authorization:** `READ_ONLY` / `SAFE_ACTIVE` (single-user measurement); `LOAD_GENERATING` for any multi-user or sustained load

| Category group | What WTE must support |
|---|---|
| **Page performance** | Load timing, rendering, paint metrics, resource loading, third-party cost. |
| **Frontend performance** | Long tasks, main-thread blocking, layout shifts, animation smoothness, memory growth in session. |
| **API/backend performance** | Endpoint latency, throughput, error rates under single-user and controlled conditions, tail latency. |
| **Resource usage** | CPU, memory, heap, garbage collection behavior, thread/process/socket/fd counts, connection pools, disk and quotas, resource leaks. |
| **Instrumentation standards** | Navigation Timing, Resource Timing, Long Animation Frames, and equivalent emerging standards. |
| **Budgets & regression** | Performance budgets, budget violation detection, baseline comparison, performance regression detection across releases. |

#### 13.20.1 Core Web Vitals

| Metric | Requirement |
|---|---|
| **LCP** (Largest Contentful Paint) | Measure, baseline, budget, and regress per page/route. |
| **INP** (Interaction to Next Paint) | Measure interaction responsiveness under realistic interaction sets. |
| **CLS** (Cumulative Layout Shift) | Measure visual stability including post-load shifts. |
| **FCP** (First Contentful Paint) | Measure first render timing. |
| **TTFB** (Time to First Byte) | Measure server/network response contribution. |
| **Long Animation Frames** | Identify scripting-caused frame stalls. |
| **Navigation & Resource Timing** | Provide the underlying timing detail behind aggregate metrics. |

> `WTE-PRD-PERF-001` — Performance measurement must record the conditions under which it was taken (environment, device profile, network profile, cache state, version, run count) so results are comparable.

> `WTE-PRD-PERF-002` — WTE must support performance budgets per route/workflow and must report violations as findings with the specific metric and threshold.

> `WTE-PRD-PERF-003` — WTE must detect performance regressions by comparing against historical baselines, and must account for measurement variance before declaring a regression.

> `WTE-PRD-PERF-004` — Performance findings must be attributable: which page, route, workflow, resource, endpoint, or third party contributed to the degradation.

> `WTE-PRD-PERF-005` — Core Web Vitals must be first-class, baseline-tracked metrics in the quality model for web targets.

> `WTE-PRD-PERF-006` — Resource and runtime testing must detect resource leaks across repeated operations, not only instantaneous consumption.

---

### 13.21 Load & Scalability Testing

**Horizon:** LONG-TERM
**Authorization:** `LOAD_GENERATING` mandatory; never implied by a public target

| Category group | What WTE must support |
|---|---|
| **Load profiles** | Smoke load, average load, expected-peak load, stress, spike, soak/endurance, volume/data-driven load. |
| **Scalability analysis** | Concurrency limits, capacity discovery, breakpoint identification, scaling behavior (horizontal/vertical), distributed load generation. |
| **Load semantics** | Realistic user behavior models, think time, ramp profiles, mixed workloads, session-based vs request-based load. |
| **Observable effects** | Latency distributions, error rates, saturation signals, resource exhaustion, degradation curves, recovery behavior after load. |

> `WTE-PRD-LOAD-001` — WTE must never generate load against a target without an explicit `LOAD_GENERATING` authorization naming the target, the maximum intensity, the time window, the environment, and the responsible party.

> `WTE-PRD-LOAD-002` — WTE must enforce hard intensity ceilings and automatic abort conditions (error-rate thresholds, saturation signals, target health degradation) during load execution.

> `WTE-PRD-LOAD-003` — Load testing must be environment-aware: production load testing must be a separately authorized, explicitly justified, and tightly limited activity, and must be blocked by default.

> `WTE-PRD-LOAD-004` — Load results must be expressed as distributions and saturation behavior, not single averages, and must be correlated with infrastructure and application telemetry where available.

> `WTE-PRD-LOAD-005` — WTE must support capacity and scalability conclusions with clearly stated assumptions and confidence, and must never present a single run as a definitive capacity statement.

---

### 13.22 Network, DNS, CDN & Edge

**Horizon:** LONG-TERM (partial support PLANNED for HTTP-level network evidence)
**Authorization:** `READ_ONLY` / `SAFE_ACTIVE`

| Category group | What WTE must support |
|---|---|
| **Connectivity** | Reachability, routing, ports, protocols, proxies, traffic capture, network errors. |
| **Network quality** | Latency, jitter, packet loss, bandwidth, network degradation behavior. |
| **DNS** | Record types (A, AAAA, CNAME, MX, TXT, NS, CAA), DNSSEC presence, TTL behavior, propagation, failover behavior. |
| **CDN / Edge** | Caching behavior, routing, edge functions, geographic delivery, invalidation, response headers, failover. |

> `WTE-PRD-NET-004` — WTE must capture network-level evidence (requests, responses, timings, failures, headers) for all web and API testing as part of the standard evidence model.

> `WTE-PRD-NET-005` — WTE must validate DNS and delivery configuration for authorized domains, including record correctness, TTL behavior, and failover assumptions where declared.

> `WTE-PRD-NET-006` — Network degradation scenarios (latency, loss, throttling) must be simulatable in controlled test environments for reliability and UX validation.

---

### 13.23 Database Testing & Migration

**Horizon:** LONG-TERM
**Authorization:** `READ_ONLY` (inspection); `MUTATING` (test data operations); production database mutation requires explicit, exceptional authorization

| Category group | What WTE must support |
|---|---|
| **Functionality** | Queries, transactions, constraints, referential integrity, stored procedures, triggers, views. |
| **Structure** | Schema validation, indexes, partitioning, expected-versus-actual structure. |
| **Concurrency** | Locking behavior, deadlocks, isolation levels, contention. |
| **Connections & performance** | Connection management, pool behavior, query performance, slow-query identification. |
| **Migration** | Forward migrations, rollback, data transformations, backward compatibility, zero-downtime compatibility. |

> `WTE-PRD-DB-001` — Database testing must operate through declared, authorized access paths with credential references, and must never assume direct production database access.

> `WTE-PRD-DB-002` — Migration testing must verify both forward and backward compatibility relevant to the deployment strategy, and must identify operations that are not safe under zero-downtime deployment.

> `WTE-PRD-DB-003` — Database observations must be correlated with application evidence (a failing query with a failing API and a failing UI flow is one investigation, not three).

> `WTE-PRD-DB-004` — Any database mutation performed by testing must be scoped, isolated, reversible where feasible, and recorded as evidence metadata.

---

### 13.24 Data Quality, Pipelines, BI & Analytics

**Horizon:** LONG-TERM
**Authorization:** `READ_ONLY` / `MUTATING` (dataset mutation in test environments only)

| Category group | What WTE must support |
|---|---|
| **Data quality dimensions** | Accuracy, completeness, consistency, validity, uniqueness, freshness, integrity, reconciliation. |
| **Pipelines** | ETL/ELT verification, batch processing, streaming transforms, transformation correctness, reconciliation across stages, warehouses and analytics pipelines. |
| **BI & analytics** | Dashboards, metrics, aggregations, filters, drilldowns, exports, charts, business calculations. |
| **Search systems** | Indexing, querying, ranking, relevance, filtering, faceting, synonyms, typo handling, freshness, search performance. |
| **Cache behavior** | Hit/miss behavior, invalidation, expiration, consistency, stale data, fallback, cache stampede behavior. |
| **Test data** | Fixtures, factories, synthetic data, seeds, masking, PII anonymization, deterministic generation, versioning, lifecycle. |

> `WTE-PRD-DATA-001` — WTE must validate data quality against declared expectations (rules, invariants, reconciliation targets) and must report deviations with the specific rule and dataset involved.

> `WTE-PRD-DATA-002` — WTE must support end-to-end data verification: that data written through an interface appears correctly in downstream systems within declared expectations.

> `WTE-PRD-DATA-003` — WTE must support BI/analytics correctness checks where business calculations can be independently derived.

> `WTE-PRD-DATA-004` — WTE must support search system evaluation: relevance expectations, ranking behavior, and search-specific quality signals.

> `WTE-PRD-DATA-005` — WTE must support cache testing as a distinct domain in network, API, and database layers, including staleness and invalidation verification.

> `WTE-PRD-DATA-006` — WTE must manage test data deterministically and must never use unmasked production personal data in generated tests or evidence without explicit authorization and configured controls.

---

### 13.25 Files, Documents, Email & Notifications

**Horizon:** PLANNED (files/documents); LONG-TERM (email/notification delivery validation)
**Authorization:** `SAFE_ACTIVE`; `MUTATING` where sending messages or modifying storage

| Domain | What WTE must support |
|---|---|
| **File & document validation** | CSV, XLSX, PDF, JSON, XML, YAML, ZIP, images, documents: encoding, MIME correctness, checksums, corruption detection, size, metadata. |
| **Upload testing** | File type validation, MIME validation, size limits, malformed/malicious files (in authorized security contexts), storage verification, scanning behavior, duplicate handling, upload recovery. |
| **Email testing** | Delivery, SMTP behavior, HTML/plain-text bodies, templates, links, OTP delivery, verification flows, attachments, headers, authentication records (SPF/DKIM/DMARC), responsive email rendering. |
| **Notifications** | Email, SMS, push, web push, chat platforms (Slack/Teams), webhooks, incident notifications. |

> `WTE-PRD-MSG-001` — WTE must validate message-producing flows (email, SMS, push, webhooks) in test environments using capture/inspection mechanisms where available, and must never send unsolicited external communications.

> `WTE-PRD-MSG-002` — WTE must validate file handling end to end: acceptance, rejection, storage, retrieval, integrity, and error behavior.

> `WTE-PRD-MSG-003` — Email and notification validation must include content correctness, link validity, rendering, and delivery authentication configuration where in scope.

---

### 13.26 Localization & Internationalization

**Horizon:** LONG-TERM
**Authorization:** `READ_ONLY` / `SAFE_ACTIVE`

| Category group | What WTE must support |
|---|---|
| **Language coverage** | Language availability, missing translations, fallback behavior, untranslated content detection. |
| **Rendering correctness** | RTL/LTR handling, Unicode correctness, text expansion, text truncation, layout breaking under localization. |
| **Formatting** | Currency, numbers, dates, times, calendars, addresses, telephone numbers per locale. |
| **Temporal correctness** | Timezones, DST transitions, locale-specific date boundaries. |

> `WTE-PRD-I18N-001` — WTE must verify localization completeness and correctness per locale, per page/workflow, and must report missing or fallback-rendered content.

> `WTE-PRD-I18N-002` — WTE must detect locale-specific rendering defects (truncation, overflow, broken layout in RTL) as objective observations.

> `WTE-PRD-I18N-003` — WTE must validate locale-sensitive formatting and timezone behavior as deterministic checks where expected values are declared.

---

### 13.27 Payments & E-Commerce

**Horizon:** LONG-TERM
**Authorization:** `MUTATING` in test/sandbox environments; real-money operations are `DESTRUCTIVE` and prohibited by default

| Domain | What WTE must support |
|---|---|
| **Payments** | Checkout flows, authorization, capture, failure handling, retry logic, refunds and partial refunds, subscriptions and recurring payments, payment webhooks, currency handling, tax behavior — against declared test/sandbox environments. |
| **E-commerce** | Catalog, products, variants, pricing, discounts, coupons, cart, wishlist, checkout, shipping, tax, inventory, orders, returns, refunds, subscriptions. |

> `WTE-PRD-PAY-001` — WTE must never trigger unauthorized real-money transactions; payment testing must use provider-sanctioned sandboxes or explicitly authorized test accounts.

> `WTE-PRD-PAY-002` — WTE must verify payment flow state machines, including failure, retry, idempotency, and webhook-driven state transitions.

> `WTE-PRD-PAY-003` — E-commerce testing must validate pricing, discount, tax, and inventory logic as business rules with reproducible calculations.

> `WTE-PRD-ECOM-001` — WTE must verify the e-commerce order lifecycle end to end (catalog → cart → checkout → order → fulfillment → return/refund) in authorized test environments, with business-rule assertions at each transition.

---

### 13.28 SEO, Content & PWA

**Horizon:** PLANNED (SEO basics); LONG-TERM (full content/CMS and PWA validation)
**Authorization:** `READ_ONLY`

| Domain | What WTE must support |
|---|---|
| **SEO** | Titles, meta descriptions, canonicals, robots directives, sitemaps, Open Graph, social metadata, structured data, hreflang, internal/external links, redirects, crawlability, indexability. |
| **Content & CMS** | Content presence, duplicate content, broken content, publishing state, drafts versus published, preview behavior, revision history, content permissions, scheduled publishing, CMS workflows. |
| **PWA / Service workers** | Manifest correctness, installability criteria, offline behavior, caching strategy, service worker lifecycle and updates, background behavior, fallbacks. |

> `WTE-PRD-SEO-001` — WTE must validate SEO fundamentals and structured data against declared expectations, and must report issues per page with evidence of the actual rendered or served content.

> `WTE-PRD-SEO-002` — WTE must validate crawlability and indexability signals — robots directives, canonical consistency, sitemaps, redirect chains, and hreflang consistency — and must report conflicts between them.

> `WTE-PRD-PWA-001` — WTE must validate PWA installability criteria, offline behavior, and service worker lifecycle (installation, update, activation, cache invalidation) as deterministic checks with cache-state evidence.

> `WTE-PRD-SEO-003` — Content validation must distinguish content defects (missing, broken, duplicate, stale) from design defects, and must link content findings to the pages and templates affected.

---

### 13.29 Mobile

**Horizon:** LONG-TERM
**Authorization:** `SAFE_ACTIVE` (interaction); `MUTATING` (state-changing app flows)

| Domain | What WTE must support |
|---|---|
| **Platforms** | Android, iOS, native, hybrid, webview-based applications, mobile browsers. |
| **Behavior** | Gestures, permissions, orientation handling, application lifecycle (background/foreground), notifications. |
| **Mobile performance** | Startup time, CPU, memory, battery impact, network usage, frame rendering (jank), storage footprint, application size. |

> `WTE-PRD-MOBILE-001` — Mobile testing must be device- and OS-version-aware, with results attributable to specific device/OS combinations.

> `WTE-PRD-MOBILE-002` — Mobile performance must be measured on real or realistically emulated devices, with the measurement conditions recorded.

> `WTE-PRD-MOBILE-003` — Mobile lifecycle behavior (interruption, backgrounding, permission changes, network transitions) must be testable as deterministic scenarios.

---

### 13.30 Desktop & Install/Upgrade/Uninstall

**Horizon:** LONG-TERM
**Authorization:** `SAFE_ACTIVE` / `INFRASTRUCTURE_MUTATING` for install/uninstall on test machines

| Domain | What WTE must support |
|---|---|
| **Platforms** | Windows, macOS, Linux; native desktop and Electron-style applications. |
| **Behavior** | Window management, OS integration, file system interactions, permission requirements. |
| **Lifecycle** | Clean install, prerequisite validation, upgrade, downgrade where supported, migration of settings/data, uninstallation, residual data detection, configuration preservation. |

> `WTE-PRD-DESKTOP-001` — Desktop testing must validate the full product lifecycle: install, first run, upgrade, and uninstall, including residual-state verification.

> `WTE-PRD-DESKTOP-002` — Desktop test execution must occur in isolated environments so that installation tests never affect a developer or user machine.

---

### 13.31 Build, Code Quality, Coverage, Mutation & CI/CD

**Horizon:** PLANNED (build, code quality, CI/CD gates); LONG-TERM (coverage intelligence, mutation testing)
**Authorization:** `SAFE_ACTIVE` / `MUTATING` (build and pipeline operations)

| Domain | What WTE must support |
|---|---|
| **Build testing** | Dependency installation, clean builds, incremental builds, production builds, reproducibility verification, bundle output inspection, artifact integrity. |
| **Code quality** | Formatting, linting, type checking, complexity analysis, dead code detection, static quality signals, convention enforcement. |
| **Code coverage** | Line, statement, function, branch, path coverage from external tooling; requirement, workflow, UI, and API coverage computed by WTE itself from application knowledge. |
| **Mutation testing** | Measuring whether the test suite actually detects deliberately introduced defects, and using mutation results to identify weak tests. |
| **CI/CD** | Pipelines, builds, test execution, quality gates, artifacts, environment promotion, rollback, protected environments, release workflows. |

> `WTE-PRD-BUILD-001` — WTE must consume build and static-analysis results rather than reimplementing build tooling, and must normalize them into the evidence and finding models.

> `WTE-PRD-BUILD-002` — WTE must compute coverage of **requirements, workflows, UI surfaces, and APIs** from application knowledge, complementing (not replacing) code-level coverage.

> `WTE-PRD-BUILD-003` — WTE must support mutation-testing results as a strength-of-suite signal that affects confidence in test results and coverage claims.

> `WTE-PRD-CICD-001` — WTE must integrate natively with CI/CD systems as a pipeline stage that produces a machine-readable quality-gate result, human-readable summary, and persisted evidence.

> `WTE-PRD-CICD-002` — WTE must support protected environments and promotion policies: which capabilities may run where, what gates protect which environments, and who may override.

> `WTE-PRD-CICD-003` — WTE itself must participate in CI/CD with predictable exit semantics (pass / warn / block), timeouts, and bounded resource usage.

---

### 13.32 Containers, Kubernetes, Infrastructure-as-Code & Cloud

**Horizon:** LONG-TERM
**Authorization:** `READ_ONLY` (inspection) / `MUTATING` / `INFRASTRUCTURE_MUTATING` (deployment, scaling, fault injection)

| Domain | What WTE must support |
|---|---|
| **Containers** | Image builds, startup behavior, health checks, networking, volumes, secrets handling, resource limits, restart and shutdown behavior, container security posture. |
| **Kubernetes** | Deployments, StatefulSets, Services, Ingress, network policies, health probes, scaling, scheduling, resource limits, secrets, ConfigMaps, failure and recovery behavior. |
| **Infrastructure as Code** | Terraform, OpenTofu, CloudFormation, Ansible, and equivalents: syntax, configuration correctness, security posture, policy compliance, drift detection, deployment behavior validation. |
| **Cloud** | AWS, Azure, GCP: identity and permissions, networking, storage, compute, policy, configuration, security posture, availability behaviors, managed services. |
| **Serverless** | Functions, event triggers, cold starts, concurrency behavior, timeouts, permissions, retries, dead-letter behavior. |

> `WTE-PRD-INFRA-001` — Infrastructure testing must be plan-first: WTE must be able to evaluate infrastructure and configuration changes before they are applied, and must distinguish planning evidence from applied evidence.

> `WTE-PRD-INFRA-002` — Any infrastructure mutation must be `INFRASTRUCTURE_MUTATING`, explicitly authorized, environment-bounded, and reversible through declared rollback paths.

> `WTE-PRD-INFRA-003` — WTE must detect infrastructure drift between declared and actual state and report it as a finding class.

> `WTE-PRD-INFRA-004` — WTE must validate deployment topologies and their failure characteristics only within authorized environments, with blast-radius limits.

> `WTE-PRD-CLOUD-001` — Cloud and Kubernetes testing must operate through least-privilege credentials, scoped to the authorized resources for the duration of the run.

> `WTE-PRD-CLOUD-002` — Serverless testing must account for platform-specific behaviors (cold start, concurrency limits, event ordering, retry semantics) as first-class expectations rather than incidental observations.

---

### 13.33 Reliability, Chaos & Disaster Recovery

**Horizon:** LONG-TERM
**Authorization:** `READ_ONLY` (verification) / `INFRASTRUCTURE_MUTATING` (chaos, failover drills) with strict blast-radius controls

| Domain | What WTE must support |
|---|---|
| **Reliability behaviors** | Retries, timeouts, circuit breakers, failover, redundancy, graceful degradation, partial failures, dependency failures. |
| **Chaos engineering** | Controlled fault injection: network faults, service failure, worker failure, database failure, cache failure, resource pressure, latency, packet loss, infrastructure failure. |
| **Disaster recovery** | Backup, restore, point-in-time recovery, failover, region recovery, database recovery, object storage recovery, configuration recovery, RTO and RPO validation. |

> `WTE-PRD-RELIAB-001` — Reliability testing must verify declared resilience behaviors (retry, timeout, circuit breaking, degradation) and report where actual behavior differs from declared behavior.

> `WTE-PRD-CHAOS-001` — Chaos testing must always operate under explicit authorization with declared blast radius, recovery conditions, abort criteria, and a responsible human operator.

> `WTE-PRD-CHAOS-002` — Chaos experiments must never run against production by default, and must never be triggered by an AI agent without explicit human authorization for the specific experiment class.

> `WTE-PRD-DR-001` — Recovery validation must verify restorability, not merely backup existence, and must report measured recovery outcomes against declared RTO/RPO targets.

> `WTE-PRD-DR-002` — Disaster recovery results must be reproduced on a schedule (drills) with historical tracking, since recovery capability degrades silently over time.

---

### 13.34 Observability, Monitoring & SLO Validation

**Horizon:** PLANNED (consumption of observability signals); LONG-TERM (monitoring and SLO validation)
**Authorization:** `READ_ONLY`

| Domain | What WTE must support |
|---|---|
| **Observability data** | Logs, metrics, traces, correlation identifiers, telemetry, health signals, instrumentation coverage and completeness. |
| **Monitoring** | Availability checks, synthetic browser journeys, API monitoring, DNS monitoring, TLS monitoring, certificate expiry, domain expiry, alerting. |
| **SLO/SLA validation** | Technical validation of availability, latency, error rate, reliability targets, and error budgets. |

> `WTE-PRD-OBS-001` — WTE must correlate its own evidence with observability data (logs, metrics, traces) using correlation identifiers where available.

> `WTE-PRD-OBS-002` — WTE must support synthetic monitoring reusing the same test definitions used in pipelines, so that production verification and pre-release validation share definitions.

> `WTE-PRD-OBS-003` — WTE must validate observability completeness itself: missing instrumentation, absent correlation IDs, and log gaps are findings, because they undermine diagnosis.

> `WTE-PRD-SLO-001` — SLO validation must distinguish **technical validation** of targets (measurable outcomes) from organizational target-setting, and must report both measurements and confidence.

---

### 13.35 Configuration, Feature Flags & Multi-Tenancy

**Horizon:** PLANNED (configuration validation); LONG-TERM (flag matrices, multi-tenant validation)
**Authorization:** `READ_ONLY` / `MUTATING` (flag state changes in authorized environments)

| Domain | What WTE must support |
|---|---|
| **Configuration** | Configuration matrices, environment variables, configuration validation, environment drift, expected-versus-actual comparison. |
| **Feature flags** | Flag matrices, gradual rollout behavior, targeting rules, fallback behavior, kill switches, interaction between flags. |
| **Multi-tenant / SaaS** | Tenant isolation, tenant configuration differences, plan/entitlement behavior, billing/usage metering, performance isolation, data isolation. |

> `WTE-PRD-CORE-019` — WTE must support the **configuration matrix as an explicit test dimension**: results must be attributable to the configuration under which they were produced.

> `WTE-PRD-CORE-020` — WTE must validate feature-flag behavior including rollout progression, targeting correctness, fallback paths, and kill-switch effectiveness.

> `WTE-PRD-CORE-021` — For multi-tenant systems, WTE must treat tenant isolation (data, configuration, entitlement, performance) as a first-class quality dimension with dedicated checks.

---

### 13.36 Distributed Systems, Concurrency, Time, Queues & Migration

**Horizon:** LONG-TERM
**Authorization:** `READ_ONLY` (analysis) / `INFRASTRUCTURE_MUTATING` (fault and partition simulation)

WTE must be able to represent and reason about the failure modes of distributed, concurrent, time-sensitive, and asynchronous systems.

| Domain | What WTE must support |
|---|---|
| **Distributed behavior** | Consensus, network partitions, replication, eventual consistency, clock problems, retries, duplicate processing, node failures, leader changes. |
| **Concurrency** | Race conditions, thread behavior, locks, asynchronous operations, deadlocks, ordering, synchronization. |
| **Time & clock** | Timezones, DST, clock drift, scheduled jobs, expiry, calendar boundaries, date changes, long-running operations. |
| **Queues & schedulers** | Scheduling, priorities, retries, ordering, concurrency, dead-letter queues, delayed jobs, duplicate jobs, recovery. |
| **Migration** | Database, cloud, platform, application, legacy, user, and data migration verification. |
| **Enterprise integration** | CRM, ERP, HRIS, identity systems, middleware, document systems, internal services. |

> `WTE-PRD-CORE-022` — WTE must be able to express distributed failure scenarios as testable expectations (for example: "a duplicate event must not double-charge") and verify them without requiring the system under test to be modified.

> `WTE-PRD-CORE-023` — Concurrency defects must be pursued through repeatable stress patterns and race-window exploration, with results reported probabilistically (observed once, intermittently observed, consistently observed).

> `WTE-PRD-CORE-024` — Time-dependent behavior must be testable through declared time controls (mock clocks, timezone configuration, scheduled run windows) rather than by waiting in real time wherever the platform supports it.

> `WTE-PRD-CORE-025` — Enterprise integration testing must validate end-to-end business processes across systems, including identity propagation and data consistency guarantees.

---

### 13.37 AI, Machine Learning, LLM, RAG & Agent Testing

**Horizon:** LONG-TERM (evaluation engine foundations PLANNED)
**Authorization:** `SAFE_ACTIVE`; agent-under-test execution with side effects is `MUTATING`/`SECURITY_ACTIVE` depending on tools granted

WTE must be able to evaluate AI systems with the same rigor it applies to conventional software: deterministic checks where they exist, structured evaluation where they do not, and explicit uncertainty everywhere.

#### 13.37.1 ML model testing

Accuracy, precision, recall, F1, calibration, robustness (perturbation, adversarial inputs), data drift and concept drift, bias and fairness across groups, latency, throughput, memory footprint, and regression against previous model versions.

#### 13.37.2 LLM application testing

Correctness against expectations, relevance, consistency across repeated runs, instruction following, structured output (including strict JSON/schema conformance), hallucination detection, safety behavior, cost per interaction, latency, model comparison, and prompt regression.

#### 13.37.3 RAG testing

Retrieval recall and precision, context relevance and coverage, faithfulness of answers to retrieved context, answer relevance, hallucination detection, citation correctness, document grounding, chunk quality, retriever regression, and reranker quality.

#### 13.37.4 AI agent testing

Planning quality, tool selection, tool arguments, tool ordering, tool execution outcomes, retry behavior, failure recovery, memory and context handling, state management, delegation, multi-agent behavior, browser actions, API actions, goal completion, latency, cost, safety, and authorization compliance.

#### 13.37.5 Agent trajectory testing

Evaluate the **sequence**, not only the outcome:

```
Task → Plan → Tool Choice → Tool Call → Observation → State Update → Next Action → Final Result
```

Expected trajectories and actual trajectories must be comparable, with deviations reported as findings.

#### 13.37.6 AI safety

Prompt injection, indirect prompt injection (from browsed content, documents, or tool output), jailbreaks, sensitive data leakage, tool abuse, unauthorized access, excessive agency, unsafe outputs, data exfiltration, and policy violations.

#### 13.37.7 AI reliability

Run-to-run variance, model variability (including version changes), tool failure handling, recovery behavior, context loss, memory errors, agent loops, non-termination, and cost overruns.

#### 13.37.8 AI grounding

Hallucination detection, citation accuracy, source attribution, evidence grounding, and identification of unsupported claims.

> `WTE-PRD-AI-001` — WTE must support evaluating AI systems as test targets, with the same evidence, finding, history, quality, and reporting models used for conventional software.

> `WTE-PRD-AI-002` — Non-deterministic targets must be evaluated with repeated runs and statistical reporting; WTE must never present a single stochastic run as a definitive verdict.

> `WTE-PRD-AI-003` — LLM and agent evaluations must be **grounded**: conclusions must cite the retrieved context, tool outputs, traces, or artifacts that support them, and unsupported claims must be flagged.

> `WTE-PRD-AI-004` — Agent trajectory evaluation must capture the full tool-call trace with arguments, observations, and state changes as evidence.

> `WTE-PRD-AI-005` — AI safety testing must include adversarial input classes (direct and indirect injection) and must verify that the system under test does not escalate privilege, leak secrets, or exceed granted agency.

> `WTE-PRD-AI-006` — AI cost and latency must be first-class metrics, since they are release-blocking characteristics of AI systems.

> `WTE-PRD-AI-007` — Evaluation criteria for subjective qualities must be explicit, versioned, and reviewable; model-based judging must be labeled as such and must be calibrated against human review where feasible.

---

### 13.38 Specialized & Extensible Domains

**Horizon:** EXTENSION
**Authorization:** inherited from the domain; safety-critical domains require conservative defaults and explicit policy

WTE's taxonomy must never become permanently closed. The following domains must be **representable** by the product model, even when WTE does not implement their testing itself:

| Domain | Nature of support |
|---|---|
| **Computer vision systems** | Image understanding, object detection, OCR where required, visual localization, layout understanding, visual anomaly detection. |
| **Audio & voice systems** | Speech recognition evaluation, speech synthesis, audio quality, pronunciation, latency, language coverage, streaming audio. |
| **Video & streaming systems** | Playback, streaming, buffering behavior, codecs, adaptive bitrate, synchronization, captions, DRM integration points, quality measurement. |
| **WebRTC & communication systems** | Signaling, audio/video paths, NAT traversal, reconnect behavior, latency, packet loss, media quality. |
| **IoT, embedded & firmware** | Device-cloud communication, firmware updates, connectivity behavior, telemetry, hardware/software integration. |
| **Protocol & telecom** | Protocol conformance, interoperability, network appliances, mobile network generations, specialized transports. |
| **Safety-critical systems** | Automotive, medical, industrial, aviation, robotics, and similar. WTE may produce evidence and enforce process requirements; **it must never claim certification or regulatory approval**. |
| **Future domains** | Blockchain/distributed ledgers, gaming, AR/VR, industrial control, and domains not yet conceived. |

> `WTE-PRD-EXT-001` — WTE must support adding a new testing domain (new target type, new capability family, new evidence types, new evaluators) without modifying the core models for targets, evidence, findings, quality, or release.

> `WTE-PRD-EXT-002` — Domain extensions must declare their authorization sensitivity, evidence schema, evaluation rules, and safety constraints through the same registry mechanisms as built-in domains.

> `WTE-PRD-EXT-003` — WTE must clearly label extension-provided results with their provenance and confidence, and must never present extension results as more authoritative than their evidence supports.

> `WTE-PRD-EXT-004` — WTE must not claim certification, regulatory compliance, or legal adequacy for any domain, including safety-critical domains.

---

### 13.39 Taxonomy → Capability → Engine Composition

The taxonomy in §13.3–§13.38 describes **risks and activities to represent**, not the number of engines to build. Many categories are served by shared engines.

Illustrative composition (the definitive composition belongs in `ARCHITECTURE.md`):

| Engine (illustrative) | Serves categories such as |
|---|---|
| **Browser Engine** | Browser automation, functional UI, some UI/UX observation. |
| **Discovery Engine** | Web surfaces, routes, assets, technology stack, API discovery. |
| **Functional Engine** | Functional behavior, business logic, workflows. |
| **UI/UX Engine** | UI observation, UX signals, layout and interaction-state checks. |
| **Visual Engine** | Screenshots, visual comparison, baselines, visual anomalies. |
| **Accessibility Engine** | WCAG-oriented scanning, ARIA, keyboard, contrast, structure. |
| **API Engine** | REST, GraphQL, gRPC, SOAP, contracts, schemas, mocking. |
| **Performance Engine** | Page/API/backend performance, Core Web Vitals, budgets. |
| **Load Engine** | Load profiles, scalability, capacity. |
| **Network Engine** | Connectivity, DNS, TLS, CDN/edge, traffic evidence. |
| **Security Engine** | Configuration, identity, authorization, session, injection classes, HTTP security. |
| **Database Engine** | Database functionality, schema, migrations, concurrency. |
| **Data Engine** | Data quality, pipelines, reconciliation, analytics. |
| **Mobile Engine** | Mobile functional and performance testing. |
| **Desktop Engine** | Desktop applications, install/upgrade lifecycle. |
| **Infrastructure Engine** | Containers, Kubernetes, IaC, cloud, serverless, deployment. |
| **AI Evaluation Engine** | ML, LLM, RAG, agent, trajectory, safety, grounding evaluation. |
| **Analysis Engine** | Correlation, root cause, impact analysis, risk, quality scoring. |

> `WTE-PRD-CORE-026` — Engine composition must be defined by reuse, platform capability, and operational characteristics — never one-engine-per-testing-category.

> `WTE-PRD-CORE-027` — All engines must produce results into the same execution, evidence, finding, history, and quality models; no engine may maintain an isolated result store.

---

### 13.40 Capability Horizons Summary

The table below summarizes the horizon classification of the domains in §13. Definitive sequencing is owned by `PHASES.md`.

| Domain (§13) | Horizon | Authorization sensitivity |
|---|---|---|
| Testing foundations & test-level vocabulary | FOUNDATIONAL | n/a (planning vocabulary) |
| Target & environment model | FOUNDATIONAL | gates all operations |
| Discovery (web) | FOUNDATIONAL | `READ_ONLY` → `SAFE_ACTIVE` |
| Application knowledge (core graph) | FOUNDATIONAL | `READ_ONLY` |
| Browser automation | FOUNDATIONAL | `SAFE_ACTIVE`, `MUTATING` |
| Functional & workflow (core) | FOUNDATIONAL | `SAFE_ACTIVE`, `MUTATING` |
| Evidence, findings, correlation, history, RCA | FOUNDATIONAL | n/a (intelligence) |
| Quality model & release readiness | FOUNDATIONAL | n/a (decision support) |
| UI observation & evaluation rules | PLANNED | `READ_ONLY` |
| UX (objective signals → subjective evaluation) | PLANNED → LONG-TERM | `READ_ONLY` |
| Visual testing & baselines | PLANNED | `READ_ONLY` |
| Accessibility (automated) → AT validation | PLANNED → LONG-TERM | `READ_ONLY` / `SAFE_ACTIVE` |
| Responsive & compatibility matrices | PLANNED | `READ_ONLY` |
| API (REST/HTTP) | PLANNED | `SAFE_ACTIVE` / `MUTATING` |
| API (GraphQL, gRPC, SOAP, realtime, messaging) | LONG-TERM | `SAFE_ACTIVE` / `MUTATING` |
| Contract & schema testing | PLANNED | `READ_ONLY` |
| Authentication/authorization/session | PLANNED → LONG-TERM | `SAFE_ACTIVE` |
| Security (passive) → security (active) | PLANNED → LONG-TERM | `READ_ONLY` → `SECURITY_ACTIVE` |
| Cryptography/TLS & HTTP security | PLANNED | `READ_ONLY` |
| Privacy | LONG-TERM | `READ_ONLY` |
| Performance & Core Web Vitals | PLANNED | `SAFE_ACTIVE` |
| Load & scalability | LONG-TERM | `LOAD_GENERATING` |
| Network, DNS, CDN/edge | LONG-TERM | `READ_ONLY` / `SAFE_ACTIVE` |
| Database & migration | LONG-TERM | `READ_ONLY` / `MUTATING` |
| Data quality, pipelines, BI, search, cache, test data | LONG-TERM | `READ_ONLY` / `MUTATING` |
| Files, documents, email, notifications | PLANNED → LONG-TERM | `SAFE_ACTIVE` / `MUTATING` |
| Localization & i18n | LONG-TERM | `READ_ONLY` |
| Payments & e-commerce | LONG-TERM | `MUTATING` (sandbox) |
| SEO, content/CMS, PWA | PLANNED → LONG-TERM | `READ_ONLY` |
| Mobile | LONG-TERM | `SAFE_ACTIVE` |
| Desktop & install lifecycle | LONG-TERM | `SAFE_ACTIVE` / `INFRASTRUCTURE_MUTATING` |
| Build, code quality, coverage, mutation, CI/CD | PLANNED → LONG-TERM | `SAFE_ACTIVE` |
| Containers, Kubernetes, IaC, cloud, serverless | LONG-TERM | `INFRASTRUCTURE_MUTATING` |
| Reliability, chaos, disaster recovery | LONG-TERM | `INFRASTRUCTURE_MUTATING` |
| Observability, monitoring, SLO validation | PLANNED → LONG-TERM | `READ_ONLY` |
| Configuration, feature flags, multi-tenancy | PLANNED → LONG-TERM | `READ_ONLY` / `MUTATING` |
| Distributed systems, concurrency, time, queues, migration, enterprise integration | LONG-TERM | `READ_ONLY` / `INFRASTRUCTURE_MUTATING` |
| AI/ML/LLM/RAG/agent evaluation | PLANNED → LONG-TERM | `SAFE_ACTIVE` → `MUTATING` |
| Vision, audio, video, WebRTC | LONG-TERM → EXTENSION | `SAFE_ACTIVE` |
| IoT, embedded, telecom, safety-critical, future domains | EXTENSION | domain-specific, conservative |

---

## 14. Application Knowledge

§13.7 defines what the knowledge model must represent. This section defines the **product requirements** for how knowledge is acquired, trusted, governed, and used.

### 14.1 Acquisition sources

Application knowledge is acquired from, at minimum:

```
Discovery (web, API, infrastructure, data)
Execution results and observations
Source code and static analysis
Repository structure and change history
Schemas (OpenAPI, GraphQL, database, protobuf, JSON Schema)
Configuration and infrastructure definitions
Observability data (logs, metrics, traces)
Human contributions (documentation, annotations, corrections)
Requirements, tickets, and user stories
```

> `WTE-PRD-KNOW-008` — WTE must record, for every knowledge assertion, its source, acquisition time, and confidence, so that knowledge can be audited and invalidated.

> `WTE-PRD-KNOW-009` — WTE must support human correction of the knowledge model, and must treat corrected knowledge as authoritative over inference within declared scope.

### 14.2 Knowledge lifecycle

> `WTE-PRD-KNOW-010` — Knowledge must be versioned over time: WTE must be able to answer "what did we know about this system at release N".

> `WTE-PRD-KNOW-011` — Knowledge that stops being observed must decay or be marked stale rather than persisting as an unverified truth.

> `WTE-PRD-KNOW-012` — Conflicting knowledge (a relationship asserted by one source and contradicted by another) must be surfaced as a conflict, never silently resolved.

### 14.3 Knowledge governance

> `WTE-PRD-KNOW-013` — Knowledge must respect authorization: facts discovered under one authorization scope must not be used to justify operations outside that scope.

> `WTE-PRD-KNOW-014` — Knowledge must be exportable and importable in a documented form so that organizations are never locked out of their own understanding of their systems.

> `WTE-PRD-KNOW-015` — Knowledge must be attributable for privacy: knowledge containing personal or sensitive information must be classified and protected like evidence.

### 14.4 How knowledge improves testing

| Knowledge | Improves |
|---|---|
| Route/component graph | Change impact analysis, test selection, UI/visual scoping. |
| API/service/database graph | Root-cause analysis, contract testing, data verification. |
| Workflow graph | Critical journey coverage, test generation, release gating. |
| Role/permission graph | Authorization matrix testing, privilege-escalation testing. |
| Test→workflow coverage | Selection, coverage reporting, gap identification. |
| Finding→component mapping | Risk scoring, regression prediction, ownership routing. |
| Change→API/component mapping | Impact analysis, targeted regression. |
| Release→change mapping | Release history, blame-free regression attribution, trend analysis. |

> `WTE-PRD-KNOW-016` — Every intelligence capability in WTE must demonstrably consume application knowledge; knowledge that is never used is a product defect.

---

## 15. Test Generation

**Horizon:** PLANNED (structural generation from discovery/schemas); LONG-TERM (requirements- and telemetry-driven generation)

### 15.1 Generation sources

Test generation must be possible from:

```
Application discovery (routes, navigation, interactive elements)
DOM and accessibility tree structure
Application knowledge graph (workflows, components, services)
OpenAPI / GraphQL / protobuf / XML schemas
JSON Schema and data schemas
Database schemas and constraints
Source code (with static analysis support)
Requirements and user stories
Existing tests (augmentation, variation, strengthening)
Historical failures (regression-oriented generation)
Production telemetry (real usage-derived scenarios)
```

### 15.2 Generation requirements

> `WTE-PRD-GEN-001` — WTE must generate test candidates from discovered structure and schemas, including positive, negative, boundary, and equivalence-class cases where the model provides enough structure.

> `WTE-PRD-GEN-002` — Every generated test must be **traceable** to the artifact or observation that justified it, and must record the generation method used.

> `WTE-PRD-GEN-003` — Generated tests must be **reviewable and editable** by humans, and must be **versionable** like any other artifact.

> `WTE-PRD-GEN-004` — Generated tests must be **auditable**: a user must be able to determine why a test exists, what it covers, and whether it has ever caught anything.

> `WTE-PRD-GEN-005` — WTE must be able to identify and retire generated tests that provide no value (always passing, redundant, or unresolvable from the current application state).

> `WTE-PRD-GEN-006` — Generation must respect authorization: generated tests must never be able to perform operations beyond the authorization class of the plan that produced them.

> `WTE-PRD-GEN-007` — WTE must support generation of assertions from observed behavior (characterization testing) and must clearly label such tests as behavior-locking rather than requirement-verifying.

> `WTE-PRD-GEN-008` — AI-assisted generation must produce tests that are executable and evidence-producing, and must never produce tests whose pass/fail cannot be objectively determined.

---

## 16. Change Impact Analysis

**Horizon:** PLANNED (VCS-based); LONG-TERM (full graph-based impact)

### 16.1 Inputs

```
Git diffs and commit metadata
Abstract syntax tree (AST) changes
Dependency graphs (code, service, package)
Route graphs and component graphs
API graphs and schema diffs
Workflow graphs
Test coverage data
Historical failure data
Deployment and release history
```

### 16.2 Requirements

> `WTE-PRD-IMPACT-001` — WTE must determine, from a change set, what can be affected: components, routes, APIs, services, workflows, and quality dimensions.

> `WTE-PRD-IMPACT-002` — Impact analysis must produce an explanation chain: change → affected artifact → affected behavior → affected workflow → risk implication.

> `WTE-PRD-IMPACT-003` — Impact analysis must distinguish **directly changed** artifacts from **transitively affected** ones, and must state the path of the relationship.

> `WTE-PRD-IMPACT-004` — Impact analysis must be usable without complete knowledge: partial knowledge must produce partial, clearly bounded impact — never fabricated confidence.

> `WTE-PRD-IMPACT-005` — Impact analysis must identify changes that affect release-blocking areas (payments, authentication, data integrity, tenant isolation) with elevated risk by policy.

> `WTE-PRD-IMPACT-006` — Impact analysis must account for infrastructure, configuration, and schema changes, not only source changes.

> `WTE-PRD-IMPACT-007` — Impact results must feed test selection (§17), risk assessment (§28), and release gating (§29).

---

## 17. Intelligent Test Selection

**Horizon:** PLANNED (rule-based selection); LONG-TERM (learning-based prioritization)

### 17.1 Selection inputs

```
Changes (what changed)
Dependencies (what depends on what)
Risk (what is risky, at what severity, in what areas)
Business criticality (workflows, revenue paths, regulated functions)
Affected workflows and users
Historical failures and recurring defects
Coverage (what is already covered and where gaps exist)
Flakiness (what cannot be trusted to signal reliably)
Execution cost (time, resources, money)
Environment (what can run where)
Release scope (what is included in this release)
Policy (what is mandated regardless of optimization)
```

### 17.2 Requirements

> `WTE-PRD-SELECT-001` — WTE must select tests based on risk and relevance rather than running the complete suite by default, subject to policy-mandated minimums.

> `WTE-PRD-SELECT-002` — Selection must be **explainable**: for every selected and every excluded test, the platform must be able to state the reason.

> `WTE-PRD-SELECT-003` — Selection must support policy override: organizations must be able to mandate test categories, specific tests, or full suites for release classes where required.

> `WTE-PRD-SELECT-004` — Selection must adapt to confidence: when knowledge is incomplete, uncertain, or the change is high-risk, WTE must widen selection rather than under-test.

> `WTE-PRD-SELECT-005` — Selection must account for flakiness: a flaky test must not be treated as trustworthy evidence of either quality or regression until its instability is resolved or explicitly quarantined by policy.

> `WTE-PRD-SELECT-006` — Selection must report its **coverage consequences**: what risk the selected set does not cover, so users can accept or reject the trade-off knowingly.

> `WTE-PRD-SELECT-007` — WTE must never use selection to silently reduce mandated release gates.

> `WTE-PRD-SELECT-008` — Selection decisions and their outcomes must be recorded historically so that selection quality can be measured and improved.

---

## 18. Execution & Orchestration

**Horizon:** FOUNDATIONAL (single-target execution, capability registry); PLANNED (parallel/distributed execution, scheduling); LONG-TERM (autonomous planning, capability matching at scale)

### 18.1 Capability registry

> `WTE-PRD-ORCH-001` — WTE must maintain a capability registry describing every capability available to the platform: identifier, description, risk class, applicable target types, environments permitted, required authorization, evidence produced, evaluators applied, configuration parameters, and cost/performance characteristics.

> `WTE-PRD-ORCH-002` — The registry must support multiple engines per capability, and must expose engine availability, version, and compatibility so that selection can be capability-driven rather than vendor-driven.

> `WTE-PRD-ORCH-003` — Capabilities must be discoverable by users and agents, and must be selectable by name, by target type, by risk class, and by quality dimension.

> `WTE-PRD-ORCH-004` — The registry must expose capability health and historical reliability so that failing or degraded engines are not silently used.

### 18.2 Capability-to-engine selection

```
TARGET
   ↓
DISCOVERY
   ↓
TEST REQUIREMENT
   ↓
RISK
   ↓
AUTHORIZATION
   ↓
CAPABILITY
   ↓
AVAILABLE ENGINE
   ↓
BEST COMPATIBLE ENGINE
   ↓
EXECUTION
```

Selection must consider: target type compatibility, protocol support, environment constraints, authorization class, required evidence types, reliability history, performance/cost, version compatibility, and determinism.

Illustrative expectations (not product bindings):

| Requirement | Illustrative engine choice |
|---|---|
| Browser end-to-end & interaction | A preferred browser automation engine, with alternatives used when constraints demand. |
| Accessibility scanning | A deterministic accessibility engine, with assisted/manual validation where automation cannot decide. |
| Performance measurement | A browser performance engine, with external measurement adapters where appropriate. |
| Load generation | A load-generation engine selected by protocol fit and scale need. |
| Security validation | Deterministic checks first; authorized specialized scanners where permitted. |
| AI evaluation | The WTE evaluation engine, with external evaluation frameworks where useful. |

> `WTE-PRD-ORCH-005` — Engine selection must produce an explainable choice, including why other compatible engines were not used.

> `WTE-PRD-ORCH-006` — WTE must degrade gracefully: when a preferred engine is unavailable, selection must fall back to a compatible engine or report the capability as unavailable — never silently skip the requirement.

### 18.3 Execution model

> `WTE-PRD-ORCH-007` — WTE must support a single execution model for all capabilities: a run has a target, environment, authorization, plan, selected capabilities, evidence, findings, and history.

> `WTE-PRD-ORCH-008` — WTE must support **queueing, scheduling, dependencies, priorities, parallelism, sharding, retries, timeouts, cancellation, resume, and checkpointing** as first-class execution behaviors.

> `WTE-PRD-ORCH-009` — WTE must support **distributed execution** across specialized workers, with capability matching (a worker only receives work it is equipped and authorized to perform).

> `WTE-PRD-ORCH-010` — Execution must be **deterministic where possible**: same inputs, same environment, same configuration should produce comparable results, and non-determinism must be recorded when it occurs.

> `WTE-PRD-ORCH-011` — Execution must be **resumable**: interrupted runs must be recoverable without re-executing completed, side-effecting operations.

> `WTE-PRD-ORCH-012` — Execution must be **isolated**: parallel executions must not interfere through shared browser state, shared data, shared credentials, or shared storage.

> `WTE-PRD-ORCH-013` — Execution must be **cancellable**: users and policies must be able to abort runs, and abort must be honored promptly, including in-flight capability steps.

> `WTE-PRD-ORCH-014` — Execution must enforce **resource limits**: timeouts, concurrency ceilings, memory/CPU bounds, and rate limits per target.

> `WTE-PRD-ORCH-015` — Execution must record complete run metadata: who/what initiated it, authorization reference, plan version, capability and engine versions, environment, configuration, and timing.

### 18.4 Worker model

> `WTE-PRD-ORCH-016` — WTE must support specialized execution capabilities (browser, discovery, API, accessibility, visual, performance, load, security, database, data, mobile, desktop, infrastructure, AI, analysis, reporting) while requiring that all workers return results into the same shared execution, evidence, and finding models.

> `WTE-PRD-ORCH-017` — Workers must be able to declare their capabilities, versions, resource requirements, and authorization classes, and must be able to be drained and upgraded without corrupting in-flight work.

> `WTE-PRD-ORCH-018` — Worker failure must be detectable, attributable, and recoverable, with the failure itself recorded as platform evidence (distinct from target defects).

### 18.5 Execution policies

> `WTE-PRD-ORCH-019` — WTE must support execution policies: maximum concurrency, maximum duration, allowed environments, allowed risk classes, retry policy, and abort conditions — enforced automatically, not by convention.

> `WTE-PRD-ORCH-020` — Policies must be versioned and auditable, and policy changes must be recorded as events affecting subsequent runs.

### 18.6 Test management model

WTE must represent the organization of testing itself, so that plans, coverage, and traceability are first-class rather than implicit in scripts.

| Entity | Meaning |
|---|---|
| **Test case** | A reusable unit of verification with intent, level, foundations, and expected outcome. |
| **Suite** | A named collection of test cases with a purpose (regression, smoke, critical journeys, etc.). |
| **Plan** | What will be executed for a given purpose: target, environment, capability set, suites, policy. |
| **Run** | An execution of a plan, with its results, evidence, and findings. |
| **Requirement** | A traceable statement of intent (from an external tracker or authored in WTE) that tests and workflows relate to. |
| **Assignment** | Who is responsible for a test, a finding, or a triage decision. |

> `WTE-PRD-ORCH-021` — WTE must support test cases, suites, plans, and runs as first-class entities that can exist independently of any particular engine, framework, or authoring format.

> `WTE-PRD-ORCH-022` — WTE must support **requirements traceability**: linking tests, workflows, and findings to requirements, and reporting coverage gaps in both directions (requirement without test, test without requirement).

> `WTE-PRD-ORCH-023` — WTE must support execution history and test status per case over time, and must retain that history across engine, framework, and version changes.

> `WTE-PRD-ORCH-024` — WTE must support importing and synchronizing tests from external test-management systems without becoming a replacement for them.

> `WTE-PRD-ORCH-025` — Test management entities must participate in authorization: a plan must resolve to exactly one authorization set before it can execute.

> `WTE-PRD-ORCH-026` — WTE must expose test-status and coverage information in a form usable by selection (§17), release gating (§29), and reporting (§30).

### 18.7 Verifying the verification platform

No testing system may assume its own correctness (`P20`). WTE must be testable by WTE.

> `WTE-PRD-PLAT-001` — WTE must have a first-class way to verify its own components: engines, adapters, rules, evaluators, the capability registry, the orchestrator, workers, evidence handling, findings, AI decisions, quality scores, and release decisions.

> `WTE-PRD-PLAT-002` — WTE's verification must use the same evidence, finding, and reporting models it applies to targets; the platform's own test results are not a special case.

> `WTE-PRD-PLAT-003` — AI-decided and model-influenced behavior must be verifiable: evaluations must be repeatable, criteria must be versioned, and changes in conclusions must be attributable to model, prompt, or data changes.

> `WTE-PRD-PLAT-004` — WTE must expose its own health, correctness signals, and self-verification results as product-visible data, so that users can judge whether platform failures influenced their results.

> `WTE-PRD-PLAT-005` — Self-verification must be honest: a component that cannot be verified must be reported as unverified rather than assumed correct.

---

## 19. Evidence Model Requirements

Evidence is the platform's ground truth. Everything downstream — findings, correlation, root cause, quality, release decisions — is only as trustworthy as the evidence beneath it.

### 19.1 Evidence lifecycle

```
OBSERVE → NORMALIZE → EVALUATE → CORRELATE → REPORT
```

The first stage produces raw observation; the second makes it uniform; the third judges it; the fourth relates it; the fifth presents it.

> `WTE-PRD-EVID-001` — WTE must normalize every observation into a common evidence model, regardless of which engine, adapter, or tool produced it.

> `WTE-PRD-EVID-002` — Evidence must never be altered after capture. Derived or corrected views must be stored as new artifacts that reference the original.

### 19.2 Evidence structure

Every evidence artifact must be capable of expressing:

| Attribute | Requirement |
|---|---|
| **Identity** | Stable identifier, content address or checksum where feasible. |
| **Source** | Engine, adapter, tool, version, and execution context that produced it. |
| **Timestamp** | Capture time, and target-observed time where different. |
| **Execution** | Run, plan, step, and attempt identifiers. |
| **Target** | Target, environment, and scope under which it was captured. |
| **Type** | Evidence class (DOM, HAR, screenshot, trace, response body, metric, log line, query result, trajectory, etc.). |
| **Metadata** | Conditions, configuration, versions, device/viewport, network profile, and any factor affecting interpretation. |
| **Storage** | Location, format, size, retention class, and access policy. |
| **Security classification** | Sensitivity level and redaction state. |

> `WTE-PRD-EVID-003` — Evidence must be **immutable and referenceable**: findings, correlations, and AI conclusions point to evidence by identifier rather than duplicating it.

> `WTE-PRD-EVID-004` — Evidence must be **sufficient**: for every failed assertion or violated rule, the platform must capture what was expected, what was observed, and enough context to reproduce the situation.

> `WTE-PRD-EVID-005` — Evidence must be **secure**: secrets, credentials, tokens, and personal data must be excluded or redacted according to policy, and classification must be recorded.

> `WTE-PRD-EVID-006` — Evidence must be **retention-governed**: each evidence class must have a declared retention policy, and expiry must be enforced and auditable.

> `WTE-PRD-EVID-007` — Evidence must be **addressable in reports**: any report can reference evidence in a way that users with permission can retrieve.

> `WTE-PRD-EVID-008` — Evidence must distinguish **target defects** from **platform failures**: an engine crash, a timeout in the test harness, or a network problem on the runner must be labeled as platform/environment evidence, never as a product defect.

> `WTE-PRD-EVID-009` — Evidence volume must be manageable: the platform must support sampling, tiered storage, and summary-with-drilldown so that evidence remains useful rather than becoming an unmanageable archive.

### 19.3 Evidence classes

At minimum, WTE must support these evidence classes:

```
Screenshots          Video recordings       DOM snapshots
Accessibility trees  HAR / network capture  Browser traces
Console output       Network requests       Network responses
API responses        Metrics                Logs
Distributed traces   Database output        Files and artifacts
Agent trajectories   Evaluation transcripts
```

> `WTE-PRD-EVID-010` — New evidence classes must be addable without changing the core evidence model (see `WTE-PRD-EXT-001`).

---

## 20. Finding Model Requirements

### 20.1 The distinction chain

```
Observation → Symptom → Finding → Root Cause → Recommendation
```

| Concept | Definition | Example |
|---|---|---|
| **Observation** | A raw, factual measurement. | `element.width = 31`, `element.height = 30`, `device = mobile`. |
| **Symptom** | An observable deviation with context, not yet judged. | Touch target below platform guidance; assert failed; response returned 500. |
| **Finding** | A judged, actionable statement of a problem, with severity, evidence, and scope. | "Interactive target is smaller than the allowed minimum on mobile viewports across 12 pages." |
| **Root cause** | The probable underlying defect or condition that explains one or more findings. | Single CSS token regression affecting all icon buttons. |
| **Recommendation** | The suggested next action. | Replace hard-coded 30px sizing with the design-system token; re-run affected checks. |

> `WTE-PRD-FIND-001` — WTE must maintain these concepts as distinct entities with distinct lifecycles, and must never treat them interchangeably in the data model, the UI, or reports.

> `WTE-PRD-FIND-002` — An observation must never be presented as a finding without an evaluation rule, a stated expectation, and a severity basis.

> `WTE-PRD-FIND-003` — A finding must never be presented as a root cause. Root-cause statements require correlation and confidence (§22).

### 20.2 Finding requirements

| Attribute | Requirement |
|---|---|
| **Identity** | Stable identifier across runs; a finding that recurs is the same finding, not a new one. |
| **Severity** | Assigned by rule and/or policy; never by AI opinion alone. |
| **Confidence** | Explicit, especially for inferred or correlated findings. |
| **Evidence** | References to supporting evidence (§19). |
| **Scope** | Affected target, environment, pages/routes, components, workflows, users/roles. |
| **Status lifecycle** | New, acknowledged, in progress, fixed, verified, reopened, accepted/won't-fix, false positive. |
| **Deduplication key** | Enables grouping of the same underlying problem across runs and engines. |
| **Ownership** | Assignable to a person, team, or component owner through integration. |
| **History** | First seen, last seen, occurrences, status transitions, and who changed what. |

> `WTE-PRD-FIND-004` — Every actionable finding must reference supporting evidence where evidence is available, and must state the rule, expectation, or observation that produced it.

> `WTE-PRD-FIND-005` — Findings must be deduplicated across runs: the same problem observed again is an occurrence of the existing finding with an updated history, not a duplicate record.

> `WTE-PRD-FIND-006` — Findings must be deduplicated across engines: the same underlying problem observed by different capabilities must be groupable into a single finding with multiple supporting evidence sources.

> `WTE-PRD-FIND-007` — Findings must support the full lifecycle including verification, reopening, acceptance with rationale, and false-positive marking — and every transition must be audited.

> `WTE-PRD-FIND-008` — Findings must be able to integrate with external defect and issue systems bidirectionally, without WTE becoming a defect tracker (`NG-14`).

> `WTE-PRD-FIND-009` — Findings must carry sufficient context to be actionable without leaving the platform: what failed, where, under what conditions, with what evidence, and what to do next.

> `WTE-PRD-FIND-010` — Findings must never be suppressed silently. Suppression, acceptance, and quarantine must be explicit, reasoned, time-bounded where appropriate, and auditable.

---

## 21. Finding Correlation

### 21.1 The correlation problem

A single underlying failure frequently produces many surface symptoms. For example:

```
API returns 500
+ console error
+ chart fails to render
+ functional assertion fails
+ screenshot shows empty dashboard
```

These are **one** problem. Without correlation, they become five tickets, five investigations, and five chances to under-prioritize the real issue.

### 21.2 Correlation requirements

> `WTE-PRD-CORR-001` — WTE must correlate related symptoms across engines, layers, and time windows into grouped findings, and must expose the group as the primary unit of investigation while retaining individual evidence.

> `WTE-PRD-CORR-002` — Correlation must use, at minimum: execution and trace identifiers, timing proximity, shared components/routes/APIs, shared network requests, shared error signatures, shared stacks/signatures, and shared deployment/change context.

> `WTE-PRD-CORR-003` — Correlation must never lose information: grouped findings must retain the individual symptoms and their evidence, and the user must be able to ungroup or re-group.

> `WTE-PRD-CORR-004` — WTE must distinguish correlation from causation in its wording and its data model, and must quantify confidence in any causal claim.

> `WTE-PRD-CORR-005` — WTE must deduplicate aggressively across runs and engines to reduce noise, and must report the reduction so users can see the value.

> `WTE-PRD-CORR-006` — WTE must support "related findings" relationships beyond identity: similar findings, findings with a shared history, and findings that tend to co-occur.

> `WTE-PRD-CORR-007` — WTE must support root-cause groups: one probable cause, its supporting findings, its affected components and workflows, and its evidence trail.

> `WTE-PRD-CORR-008` — Correlation must be explainable: a user must be able to see why two symptoms were grouped and what evidence supports the grouping.

---

## 22. Root-Cause Intelligence

**Horizon:** PLANNED (rule-based, single-layer); LONG-TERM (cross-layer, AI-assisted with evidence grounding)

### 22.1 Correlation inputs

Root-cause analysis must be able to draw on:

```
Browser evidence (DOM, console, traces, screenshots, video)
Network evidence (requests, responses, timings, failures)
API evidence (status, payloads, schema violations)
Database evidence (query results, locks, errors)
Logs (application, infrastructure, security)
Metrics (resource, latency, error rates)
Distributed traces (spans, service dependencies)
Source changes (diffs, commits, blame-free attribution)
Deployments and releases (what version is running where)
Historical failures (has this happened before, under what change)
Application dependencies (what talks to what)
```

### 22.2 Outputs

Every root-cause assessment must produce:

```
Probable cause
Confidence (with basis for the confidence)
Supporting evidence (references)
Affected component(s)
Affected workflow(s)
Suggested next action
```

### 22.3 Requirements

> `WTE-PRD-RCA-001` — WTE must produce probable root causes with confidence and evidence, and must always present them as hypotheses unless deterministic evidence establishes causation.

> `WTE-PRD-RCA-002` — WTE must correlate across layers: a browser symptom must be traceable to network, API, service, database, or change-level causes where evidence supports it.

> `WTE-PRD-RCA-003` — Root-cause analysis must consume historical failures: if the same signature occurred before and was resolved by a known change, that history must inform the current hypothesis.

> `WTE-PRD-RCA-004` — WTE must identify **affected scope**: components, workflows, tenants, roles, and environments impacted by a cause.

> `WTE-PRD-RCA-005` — WTE must recommend next actions that are specific and evidence-driven (which artifact to inspect, which test to run, which change to review), not generic advice.

> `WTE-PRD-RCA-006` — WTE must be honest when it cannot determine a cause: "insufficient evidence" with the evidence gaps listed is a valid and required output.

> `WTE-PRD-RCA-007` — Root-cause accuracy must be measurable over time by comparing hypotheses with confirmed resolutions, and the measurement results must be visible to users.

---

## 23. Historical Intelligence

### 23.1 The historical model

Runs must not be isolated events. WTE must retain and reason over:

```
Projects · Targets · Environments · Releases · Runs · Executions ·
Tests · Findings · Evidence references · Metrics · Baselines ·
Changes · Root causes · Quality scores
```

### 23.2 Historical capabilities

| Capability | Description |
|---|---|
| **Regression detection** | Something that passed before now fails. |
| **New issue detection** | A finding never seen before appears. |
| **Resolved issue detection** | A previously failing check now passes. |
| **Reopened issue detection** | A resolved finding recurs. |
| **Flakiness detection** | A test's result is unstable independent of changes. |
| **Performance regression** | A metric degrades against an established baseline. |
| **Baseline evolution** | Baselines are versioned and changes are explainable. |
| **Recurring failure detection** | Patterns of failures repeating across releases or environments. |
| **Root-cause patterns** | Recurring causes across findings and systems. |
| **Risk prediction** | Predicted risk areas based on history. |
| **Test prioritization** | Historical value influencing selection. |

### 23.3 Requirements

> `WTE-PRD-HIST-001` — WTE must store and compare runs across time, releases, environments, and configuration matrices.

> `WTE-PRD-HIST-002` — WTE must maintain baselines (functional, visual, performance, accessibility, security posture) as explicit, versioned, owned artifacts.

> `WTE-PRD-HIST-003` — WTE must classify every finding occurrence as new, recurring, reopened, or resolved with respect to history, and must present that classification prominently.

> `WTE-PRD-HIST-004` — WTE must detect and report trends (improving, degrading, stable) with the data window and method used.

> `WTE-PRD-HIST-005` — WTE must correlate history with change context so that regressions can be attributed to candidate changes without asserting blame.

> `WTE-PRD-HIST-006` — History must survive infrastructure changes: retention, export, and import of historical intelligence must be supported.

> `WTE-PRD-HIST-007` — Historical data must respect retention and privacy policy while preserving the longitudinal signals the platform depends on.

---

## 24. Flaky Test Intelligence

### 24.1 The problem

A flaky test is worse than a missing test: it destroys trust in the entire signal. WTE must identify, characterize, and manage flakiness as a first-class product concern.

### 24.2 Detection signals

```
Pass/fail history across runs
Timing variance
Environment correlation (which environment, which worker, which region)
Browser/device correlation
Network correlation
Selector stability and element-resolution variance
Duration variance
Failure clustering patterns
Retry outcomes (passes on retry vs. fails consistently)
```

### 24.3 Requirements

> `WTE-PRD-FLAKY-001` — WTE must compute a flakiness assessment per test based on history, not on a single run.

> `WTE-PRD-FLAKY-002` — WTE must attempt to **explain** flakiness: timing, ordering, shared state, environment contention, network variability, test data collisions, or genuine application non-determinism.

> `WTE-PRD-FLAKY-003` — WTE must distinguish **test flakiness** from **application non-determinism**: a genuinely intermittent product defect is not a flaky test, and must not be quarantined as one.

> `WTE-PRD-FLAKY-004` — WTE must provide quarantine as an explicit, auditable, time-bounded action with an owner and a review date — never a silent skip.

> `WTE-PRD-FLAKY-005` — WTE must ensure quarantined tests do not silently reduce quality coverage: quarantined coverage must be visible in coverage and release reporting.

> `WTE-PRD-FLAKY-006` — Flakiness intelligence must feed test selection: flaky tests must be deprioritized for signal, prioritized for repair.

> `WTE-PRD-FLAKY-007` — WTE must track flakiness trends to show whether the suite is stabilizing or degrading.

---

## 25. Self-Healing

**Horizon:** LONG-TERM
**Authorization:** `SAFE_ACTIVE` for repairs; all repairs audited

### 25.1 What may be repaired

```
Selectors and locators
Text matching strategies
Role-based locators
Visual locators
Timing and wait conditions
Element resolution strategy
```

### 25.2 The mandated repair pipeline

Self-healing must never be silent. The required flow is:

```
Failure
   ↓
Candidate repair (proposed alternative locator/timing/strategy)
   ↓
Confidence score
   ↓
Validation (does the repair behave correctly on the intended element?)
   ↓
Re-run of affected test(s)
   ↓
Repair recorded (versioned, audited, reversible, with evidence)
```

> `WTE-PRD-HEAL-001` — WTE must never silently change a selector, locator, or wait strategy and continue as if nothing happened.

> `WTE-PRD-HEAL-002` — Every repair must be versioned, audited, confidence-scored, reversible, and re-tested before being treated as an accepted change.

> `WTE-PRD-HEAL-003` — Repairs must be reviewable by humans, and policy must determine whether a repair is auto-accepted, requires approval, or is only proposed.

> `WTE-PRD-HEAL-004` — A repair must never change test **intent**: if the intended element cannot be identified with sufficient confidence, the correct outcome is a reported failure, not a guess.

> `WTE-PRD-HEAL-005` — Repairs must be linked to evidence showing the failure, the candidates considered, and the validation result.

> `WTE-PRD-HEAL-006` — WTE must track the effectiveness of repairs over time and must identify repairs that cause subsequent instability.

> `WTE-PRD-HEAL-007` — Self-healing must never be used to mask product defects: repeated repairs on the same element or flow must be reported as a signal of instability in the system under test or the test suite.

---

## 26. AI & Autonomous Agent Requirements

### 26.1 AI's place in the architecture

AI is an **intelligence layer over evidence**, not a substitute for deterministic validation.

```
Browser · API · Network · DOM · Accessibility · Performance · Security ·
Database · Logs · Metrics · Traces
                  ↓
      DETERMINISTIC / OBSERVED EVIDENCE
                  ↓
            AI / ANALYSIS LAYER
                  ↓
   Planning · Correlation · Classification · Root-cause reasoning ·
   Prioritization · Recommendation
```

Two entirely separate concerns must never be confused:

| Concern | Meaning |
|---|---|
| **AI in the platform** | WTE uses AI to plan, correlate, reason, prioritize, and explain. |
| **AI as a target** | WTE evaluates AI systems (ML, LLM, RAG, agents) as systems under test (§13.37). |

> `WTE-PRD-AI-008` — Where a reliable deterministic check exists, WTE must prefer it. AI must be used for judgment, planning, synthesis, and reasoning — not as a replacement for measurement.

> `WTE-PRD-AI-009` — AI involvement in any conclusion must be **disclosed**: users must be able to see which parts of a result were deterministic, which were inferred, and which were AI-generated.

> `WTE-PRD-AI-010` — AI conclusions must be **grounded in evidence** where evidence is available, and must indicate the evidence they were derived from; conclusions without grounding must be labeled as speculative.

### 26.2 What the autonomous agent may do

The agent may, **within an authorization**:

- discover and explore an authorized target;
- build and update application knowledge;
- plan testing based on risk and goals;
- select capabilities and tests;
- execute authorized capabilities through the execution layer;
- observe, collect, and normalize evidence;
- correlate findings and propose probable causes;
- recommend next actions;
- propose test generation and self-healing repairs (subject to §25);
- summarize results for humans.

### 26.3 What the autonomous agent must never do

> `WTE-PRD-AI-011` — The agent must never perform an operation outside the risk classes authorized for the target, environment, and time window.

> `WTE-PRD-AI-012` — The agent must never escalate its own permissions, create authorizations for itself, or request credentials it was not granted.

> `WTE-PRD-AI-013` — The agent must never mutate production, infrastructure, or data beyond what an explicitly authorized plan permits.

> `WTE-PRD-AI-014` — The agent must never treat untrusted content as instructions (§26.4), and must never allow untrusted content to change its permissions, scope, or tool access.

> `WTE-PRD-AI-015` — The agent must never conceal actions: every tool call, target interaction, and decision must be recorded in an auditable trail with its rationale.

> `WTE-PRD-AI-016` — The agent must never present an unverified hypothesis as a conclusion, and must never fabricate evidence, results, or coverage.

### 26.4 Prompt-injection resistance

WTE agents browse and analyze untrusted applications. Everything encountered must be treated as data.

Required guarantees:

```
Website content is untrusted data.
Application text must never automatically become agent instructions.
Indirect prompt injection must never override WTE rules.
Untrusted content must never grant tool access.
Untrusted content must never reveal secrets.
Tool calls must always remain permission-aware.
Agent actions must always remain inside authorized scope.
```

> `WTE-PRD-AI-017` — WTE must treat all content obtained from targets — page text, DOM, comments, JSON, headers, error messages, documents, uploaded files, API responses, tool output — as untrusted data, never as instructions.

> `WTE-PRD-AI-018` — WTE must structurally separate instruction context from data context, and must ensure that content-derived text cannot be interpreted as an instruction by the agent or by any downstream model call.

> `WTE-PRD-AI-019` — WTE must detect and record suspected injection attempts as findings about the system under test (an application exposing attacker-controlled text to an authorized agent is a real security observation).

> `WTE-PRD-AI-020` — Prompt-injection defenses must not rely on the model alone: permission checks, scope enforcement, and tool gating must be enforced outside the model, by the platform.

### 26.5 Autonomy ladder

Autonomy is introduced in stages. Each stage has increasing requirements.

| Stage | Autonomy level | Requirements before enabling |
|---|---|---|
| 1 | **Assisted** — agent recommends; human initiates every execution. | Full audit trail; capability registry; authorization model. |
| 2 | **Supervised autonomy** — agent discovers, plans, and requests approval. | Explainable plans; scope enforcement; evidence capture. |
| 3 | **Bounded autonomy** — agent executes approved capability classes within policy. | Execution policies, abort conditions, resource limits, kill switch. |
| 4 | **Continuous autonomy** — agent operates on schedule, within standing authorizations. | Full auditability, drift detection, cost/rate governance, incident review process. |
| 5 | **Investigative autonomy** — agent pursues declared goals with adaptive planning. | All above plus: budget caps, blast-radius controls, human escalation paths, and measured accuracy of its conclusions. |

> `WTE-PRD-AI-021` — Autonomy must be granted per target, per environment, per risk class, and per stage — never globally by default.

> `WTE-PRD-AI-022` — WTE must provide a **kill switch** that immediately halts agent activity at any stage, and must support per-target and platform-wide abort.

> `WTE-PRD-AI-023` — Autonomous operation must be budgeted: time, request volume, generated load, and AI cost must be bounded by policy and enforced by the platform.

> `WTE-PRD-AI-024` — Autonomous conclusions must be reviewable after the fact: WTE must retain the plan, the actions, the evidence, and the reasoning chain for every autonomous run.

> `WTE-PRD-AI-025` — WTE must measure autonomous behavior quality (plan usefulness, investigation success, false conclusions) and must reduce autonomy where measured quality is insufficient.

### 26.6 AI quality requirements

> `WTE-PRD-AI-026` — Model-assisted classification and correlation must be versioned and reproducible: the platform must record which model and configuration produced a conclusion.

> `WTE-PRD-AI-027` — AI-produced conclusions must be overridable by human judgment, and overrides must feed learning (without silently rewriting history).

> `WTE-PRD-AI-028` — WTE must not use AI to fill gaps in evidence. Missing evidence must be reported as missing.

---

## 27. Authorization & Safe Execution

**This section states product-level requirements. The detailed trust and permission model belongs in `SECURITY.md`.**

### 27.1 Why authorization is a product feature

WTE contains powerful capabilities: it browses, executes, loads, probes, mutates, and — in some domains — can affect real infrastructure. A public URL is not permission. For WTE, authorization is not a security feature bolted on afterwards; it is a product capability that users interact with directly.

### 27.2 Operation risk classes

Every capability and every operation must be classified into one of the following risk classes:

| Class | Meaning | Examples |
|---|---|---|
| `READ_ONLY` | Observation without altering the target. | Navigation, discovery, screenshots, header inspection, metrics collection. |
| `SAFE_ACTIVE` | Interaction that is expected to be harmless and reversible in test data. | Form entry with test data, keyboard interaction, running an existing test suite. |
| `MUTATING` | Changes state that persists beyond the interaction. | Creating accounts, placing test orders, editing records, sending notifications. |
| `LOAD_GENERATING` | Creates traffic volumes that can degrade a target. | Any load, stress, spike, or soak testing. |
| `SECURITY_ACTIVE` | Actively probes for vulnerabilities. | Injection testing, auth bypass attempts, fuzzing, active scanning. |
| `INFRASTRUCTURE_MUTATING` | Changes infrastructure or deployment state. | Applying IaC changes, scaling, restarting workloads, chaos experiments. |
| `DESTRUCTIVE` | Can cause irreversible loss or real-world effect. | Data deletion, production mutation, real-money transactions. |

> `WTE-PRD-AUTH-001` — Every capability must declare exactly one primary risk class; operations that escalate must declare their escalation conditions.

> `WTE-PRD-AUTH-002` — WTE must refuse to execute any operation that exceeds the effective authorization for the target and environment, and refusal must be explicit, reasoned, and recorded.

> `WTE-PRD-AUTH-003` — Risk class authorization must be granted per target, per environment, per scope, and per time window, and must identify the authorizing party.

> `WTE-PRD-AUTH-004` — Higher-risk classes must never be granted implicitly by lower-risk grants.

### 27.3 Target authorization

Authorization must express, at minimum:

```
Target identity and endpoints
Environment
Allowed risk classes
Scope (allowed and forbidden: domains, paths, services, accounts, resources)
Time window and expiry
Responsible party and approver
Conditions and constraints (rate limits, maximum intensity, data handling rules)
Notification and escalation requirements
```

> `WTE-PRD-AUTH-005` — WTE must require an explicit authorization artifact before discovery or execution begins, and must include its reference in every run record.

> `WTE-PRD-AUTH-006` — WTE must support authorization verification: confirming that a target is actually owned or authorized (for example, via a challenge mechanism or a verified claim) before higher-risk classes are permitted.

> `WTE-PRD-AUTH-007` — WTE must expire authorizations and must re-require authorization for continued autonomous operation beyond the declared window.

> `WTE-PRD-AUTH-008` — WTE must support revocation, and revocation must take effect within a bounded time for both in-flight and future work.

> `WTE-PRD-AUTH-009` — WTE must make the effective authorization visible to the user before execution, in plain terms: what will run, where, at what risk class, under whose authority, until when.

### 27.4 Required safety controls

> `WTE-PRD-AUTH-010` — **Scope boundaries** must be enforced at the request level, not merely at the planning level.

> `WTE-PRD-AUTH-011` — **Domain restrictions** must prevent a run from following redirects, link targets, or embedded resources outside declared scope without explicit permission.

> `WTE-PRD-AUTH-012` — **Environment awareness** must prevent accidental production impact: production must be recognizable, and production-restricted capability classes must be blocked unless separately authorized.

> `WTE-PRD-AUTH-013` — **SSRF protection** must prevent agent- or user-directed requests from reaching unintended internal networks, metadata services, or private address ranges.

> `WTE-PRD-AUTH-014` — **Private-network controls** must ensure that LAN and internal targets require explicit authorization and are never reachable by default from hosted execution.

> `WTE-PRD-AUTH-015` — **Permission checks** must occur at execution time, not only at plan time, so that revoked or expired authority stops work in progress.

> `WTE-PRD-AUTH-016` — **Secret safety** must ensure that credentials are referenced, resolved at execution, never persisted in plaintext, never written to evidence, and never included in reports (see §27.6).

> `WTE-PRD-AUTH-017` — **Auditability** must record every privileged action: authorization used, capability invoked, engine used, target touched, scope applied, decision rationale, and outcome.

> `WTE-PRD-AUTH-018` — **Rate limits** must be enforced per target, per capability, and per authorization, and must be respected by retries and parallel workers.

> `WTE-PRD-AUTH-019` — **Resource limits** must bound execution: maximum concurrency, maximum duration, maximum data volume, and maximum generated traffic.

> `WTE-PRD-AUTH-020` — **Blast-radius controls** must ensure that a failure, misconfiguration, or runaway execution cannot harm beyond a declared boundary — with automatic abort as the default response to exceeding limits.

### 27.5 Public targets are not automatically authorized

> `WTE-PRD-AUTH-021` — A publicly reachable system must never be treated as authorized for penetration testing, stress testing, destructive testing, or infrastructure mutation.

> `WTE-PRD-AUTH-022` — WTE must apply the least-invasive capable approach by default for any unclassified target, and must require explicit human authorization to exceed it.

> `WTE-PRD-AUTH-023` — WTE must never operate against third-party systems that are outside the user's declared responsibility, even when technically reachable.

### 27.6 Secrets

> `WTE-PRD-AUTH-024` — WTE must never store secrets in plaintext in configuration, run definitions, evidence, logs, or reports.

> `WTE-PRD-AUTH-025` — Secrets must be referenced by identifier, resolved only at execution time, and scoped to the narrowest viable lifetime and audience.

> `WTE-PRD-AUTH-026` — WTE must detect accidental secret exposure in captured evidence (for example, tokens in URLs, headers, or application responses) and must redact it at capture time.

> `WTE-PRD-AUTH-027` — WTE must support rotation of test credentials without rewriting test definitions.

### 27.7 Human oversight

> `WTE-PRD-AUTH-028` — Higher-risk classes must support an approval workflow, where the requester and approver can be different parties, and the approval is recorded.

> `WTE-PRD-AUTH-029` — WTE must provide an activity view showing what the platform has done, is doing, and is permitted to do against every target.

> `WTE-PRD-AUTH-030` — WTE must surface "near-miss" events: refused operations, scope violations attempted, aborted runs, and limit breaches — as first-class security observations about the platform's own operation.

---

## 28. Quality Model

### 28.1 Dimensions

WTE must eventually evaluate quality across dimensions including:

```
Functional      UI/UX          Visual          Accessibility
API             Performance    Security        Reliability
Compatibility   SEO            Data quality    Coverage
AI quality
```

> `WTE-PRD-QUAL-001` — WTE must organize quality results by dimension, and every reported score must be decomposable to the findings, evidence, and rules that produced it.

> `WTE-PRD-QUAL-002` — WTE must not collapse quality into a single naive average. Any aggregate must be computed by an explicit, documented, configurable model.

### 28.2 Scoring inputs

Scores may consider:

```
Severity of findings
Confidence in findings
Business criticality of affected areas
Affected workflows and users
Frequency and recurrence
Regression status (new, recurring, reopened, resolved)
Historical recurrence patterns
Coverage of the dimension (what was actually tested)
Environment (production-like, staging, test)
Release policy (thresholds, mandatory dimensions)
```

> `WTE-PRD-QUAL-003` — Scores must be **explainable**: users must be able to see which inputs contributed, in what proportion, and why a score changed between runs.

> `WTE-PRD-QUAL-004` — Scores must be **comparable**: the same model applied to comparable runs must produce comparable results, and model changes must be versioned so that score changes are attributable to the model or to the system.

> `WTE-PRD-QUAL-005` — Scores must be **honest about coverage**: a dimension that was not tested must be reported as untested, not as passing.

> `WTE-PRD-QUAL-006` — Coverage (what was tested) must be a first-class input to confidence in every quality statement, including the overall assessment.

> `WTE-PRD-QUAL-007` — Quality models must be **configurable per organization and per project**, with safe defaults that avoid encouraging a false sense of security.

> `WTE-PRD-QUAL-008` — WTE must never hide evidence behind an opaque score: every score must lead to the evidence, never the reverse.

> `WTE-PRD-QUAL-009` — Quality trends must be tracked over time per dimension, with the data window and confidence of the trend disclosed.

> `WTE-PRD-QUAL-010` — WTE must distinguish **absolute quality** (how good is the system) from **change in quality** (did this release improve or degrade it), and must never conflate the two.

---

## 29. Release Readiness

### 29.1 The verdict

WTE must eventually produce, for a release candidate, one of three outcomes:

```
READY
CONDITIONALLY READY
NOT READY
```

### 29.2 Inputs

Release gates may consider:

```
Critical and high-severity findings
Functional regressions
Critical workflow results
Security posture and findings
Accessibility conformance
Performance against budgets and baselines
Reliability and resilience results
Coverage and untested areas
Deployment and environment status
Required policies and mandatory checks
Accepted exceptions and waivers
Historical context (recurrence, trend, known issues)
```

### 29.3 Requirements

> `WTE-PRD-REL-001` — WTE must produce a release verdict only when the evidence required by the applicable policy exists; missing required evidence must produce `NOT READY` or an explicit `INSUFFICIENT EVIDENCE` state, never a default pass.

> `WTE-PRD-REL-002` — Every verdict must explain: what passed, what failed, what blocked the release, which findings influenced the decision, which evidence supports it, which exceptions exist, and who approved them.

> `WTE-PRD-REL-003` — `CONDITIONALLY READY` must require explicit conditions: which findings are accepted, by whom, with what rationale, and with what follow-up deadline.

> `WTE-PRD-REL-004` — Waivers and exceptions must be explicit, time-bounded, owner-attributed, and auditable, and must be visible in future release comparisons.

> `WTE-PRD-REL-005` — Release policies must be versioned and configurable per release class (hotfix, patch, minor, major, emergency) and per environment.

> `WTE-PRD-REL-006` — WTE must support comparison between releases: what changed in quality, what was fixed, what regressed, what remained open from the previous release.

> `WTE-PRD-REL-007` — WTE must record every release verdict with its full evidence package and policy version, so decisions remain reproducible after the fact.

> `WTE-PRD-REL-008` — WTE must never claim a release is safe; it must state, in evidence-backed terms, the assessed readiness and the residual risk that remains.

> `WTE-PRD-REL-009` — Release readiness must be consumable programmatically (quality gate result) and by humans (explainable report), from the same computation.

---

## 30. Reporting

### 30.1 Report families

WTE must eventually support reports for:

```
Executive summary          Functional        UI/UX            Visual
Accessibility              API               Performance      Security
SEO                        Database          Reliability      Compatibility
Infrastructure             AI / LLM / RAG    Agent behavior   Release readiness
Compliance evidence
```

### 30.2 Output formats

Possible formats include HTML, JSON, CSV, XLSX, PDF, JUnit XML, SARIF, and Markdown.

> `WTE-PRD-REPORT-001` — WTE must not require every format in the first release; formats must be added according to user need and interoperability value.

> `WTE-PRD-REPORT-002` — Every report must reference the evidence behind its conclusions, and must be reproducible from the stored run data.

> `WTE-PRD-REPORT-003` — Reports must state their scope explicitly: target, environment, configuration, authorization reference, run window, capability set, and engine versions.

> `WTE-PRD-REPORT-004` — Reports must distinguish measured facts, evaluated findings, inferred correlations, and AI-generated summaries, and must never blend them indistinguishably.

> `WTE-PRD-REPORT-005` — Reports must respect evidence security classification: sensitive evidence must be redacted or access-controlled according to policy.

> `WTE-PRD-REPORT-006` — WTE must produce **machine-readable** results suitable for CI/CD gating and external tooling, in addition to human-readable reports.

> `WTE-PRD-REPORT-007` — Compliance-oriented reports must present technical evidence and mappings to control frameworks where configured, and must never assert legal or regulatory compliance (`NG-9`).

> `WTE-PRD-REPORT-008` — Reports must be shareable in a way that preserves traceability: a recipient must be able to determine what produced each conclusion.

> `WTE-PRD-REPORT-009` — WTE must support scheduled and event-triggered report generation (per run, per release, per period).

---

## 31. Dashboards

### 31.1 Dashboard domains

WTE dashboards may expose:

```
Overall quality            Functional quality      UI/UX quality
Accessibility              API quality             Performance
Security                   Reliability             Coverage
Pass rate                  Failure rate            Flakiness
Findings                   Severity distribution   Regressions
Execution duration         Queue status            Worker utilization
Quality trends             Release readiness
```

### 31.2 Requirements

> `WTE-PRD-DASH-001` — The interface must never hide evidence behind opaque AI scores. Every displayed metric must be drillable to the findings and evidence that produced it.

> `WTE-PRD-DASH-002` — Dashboards must distinguish "not tested" from "tested and passing", and must make coverage gaps visible, not visually neutral.

> `WTE-PRD-DASH-003` — Dashboards must present trends with their data windows, and must avoid implying certainty from thin data.

> `WTE-PRD-DASH-004` — Dashboards must support the primary personas (§9): rapid developer feedback (change-focused), QA triage (finding-focused), manager oversight (trend-focused), and release decisions (gate-focused).

> `WTE-PRD-DASH-005` — Dashboards must be target-, environment-, release-, and configuration-aware, so that users always know what they are looking at.

> `WTE-PRD-DASH-006` — Dashboard data must be consistent with API and report data: the same run must never produce conflicting numbers in different surfaces.

> `WTE-PRD-DASH-007` — User experience details — layout, interaction patterns, navigation — are owned by `DESIGN.md`. This section defines only what must be observable and trustworthy.

---

## 32. Integrations

### 32.1 Integration categories

WTE must support extensible integrations in the following categories:

| Category | Examples of concerns |
|---|---|
| **Source control** | Change context, pull-request integration, commit attribution. |
| **CI/CD** | Pipeline stages, quality gates, artifacts, promotion, rollback. |
| **Project management** | Work item linkage, planning context, requirement traceability. |
| **Defect management** | Bidirectional finding synchronization, ownership, status. |
| **Test management** | Test case, suite, plan, and execution synchronization. |
| **Documentation** | Requirements, specifications, runbooks as knowledge sources. |
| **Observability** | Logs, metrics, traces, release markers, incident context. |
| **Incident management** | Incident linkage and post-incident evidence packages. |
| **Communication** | Notifications, alerts, summaries to team channels. |
| **Cloud platforms** | Credentials, resources, inventory, deployment context. |
| **Enterprise systems** | Identity, ITSM, data and process systems. |

### 32.2 Requirements

> `WTE-PRD-INTEG-001` — Integrations must be adapter-driven: no integration may be a product requirement tied to a single vendor.

> `WTE-PRD-INTEG-002` — Integrations must be bidirectional where the external system's purpose requires it (for example, defect status changes flowing back as finding lifecycle transitions).

> `WTE-PRD-INTEG-003` — Integrations must never be a prerequisite for core functionality: WTE must work standalone, with integrations adding value.

> `WTE-PRD-INTEG-004` — Integrations must authenticate with least privilege and must never require broader access than the integration's function needs.

> `WTE-PRD-INTEG-005` — Integration failures must be visible, non-destructive, and recoverable, and must not corrupt WTE's own state.

> `WTE-PRD-INTEG-006` — All integrations must respect authorization: data flowing to external systems must honor evidence classification and scope.

> `WTE-PRD-INTEG-007` — WTE must expose a public contract for building new integrations, and the contract must be versioned and stable.

---

## 33. Non-Functional Requirements

Numeric targets are deliberately not invented here. Where a target is required but undecided, the value is `TBD` and must be resolved before the relevant capability is declared generally available.

| ID | Attribute | Requirement |
|---|---|---|
| `WTE-PRD-NFR-001` | **Reliability** | WTE must operate reliably as shared infrastructure; partial failures must degrade gracefully rather than corrupting runs, evidence, or findings. |
| `WTE-PRD-NFR-002` | **Scalability** | WTE must scale in target count, concurrent runs, evidence volume, and worker count, with horizontal scaling of execution. Targets: `TBD`. |
| `WTE-PRD-NFR-003` | **Performance** | Interaction and result latency must support interactive developer workflows; large-scale execution must be throughput-oriented. Targets: `TBD`. |
| `WTE-PRD-NFR-004` | **Security** | WTE must follow least privilege, defense in depth, secure defaults, and never store secrets in plaintext. |
| `WTE-PRD-NFR-005` | **Isolation** | Tenants, projects, runs, and browser/worker contexts must be isolated so that no execution can observe or affect another's data. |
| `WTE-PRD-NFR-006` | **Extensibility** | New capabilities, engines, adapters, evidence types, and domains must be addable without core redesign. |
| `WTE-PRD-NFR-007` | **Interoperability** | WTE must interoperate through standard formats and protocols rather than proprietary lock-in. |
| `WTE-PRD-NFR-008` | **Portability** | WTE must be deployable across local, containerized, cloud, and enterprise environments, including air-gapped or restricted networks. |
| `WTE-PRD-NFR-009` | **Auditability** | Every privileged or autonomous action must be recorded with actor, authority, scope, and outcome. |
| `WTE-PRD-NFR-010` | **Observability** | WTE must expose its own health, queue state, worker state, and execution telemetry, and must be diagnosable using its own principles. |
| `WTE-PRD-NFR-011` | **Determinism** | Where determinism is achievable (same inputs, environment, configuration), WTE must produce comparable results and must record when it does not. |
| `WTE-PRD-NFR-012` | **Recoverability** | Runs, evidence, and history must survive process, worker, and infrastructure failures without loss of already-captured evidence. |
| `WTE-PRD-NFR-013` | **Maintainability** | The platform must be understandable and modifiable by its own team: shared models, explicit contracts, and no capability-specific silos. |
| `WTE-PRD-NFR-014` | **Vendor independence** | No core product requirement may depend on a single external vendor. |
| `WTE-PRD-NFR-015` | **Cost governance** | Execution and AI costs must be attributable per target, project, and run, and must be boundable by policy. |
| `WTE-PRD-NFR-016` | **Data governance** | Evidence and knowledge must be classified, retention-governed, exportable, and deletable in accordance with policy. |
| `WTE-PRD-NFR-017` | **Accessibility of the product itself** | WTE's own user interfaces must meet the accessibility standards it tests for. |
| `WTE-PRD-NFR-018` | **Time to first value** | A new target must be able to produce a first useful, safe result without expert configuration. Target: `TBD`. |

---

## 34. Product Success Metrics

Metrics must measure whether WTE is delivering the value defined in §5. Numerical targets are not invented here; unapproved values are `TBD`.

### 34.1 Detection

| Metric | Definition |
|---|---|
| Known regression detection | Share of intentionally introduced or historically known regressions detected by WTE. |
| Critical workflow coverage | Share of declared critical workflows covered by executed tests. |
| False-positive rate | Share of findings later confirmed as not real. `TBD` target. |
| Duplicate-finding reduction | Reduction in distinct finding records relative to raw symptoms. |

### 34.2 Efficiency

| Metric | Definition |
|---|---|
| Time to useful results | Time from target submission to first actionable finding. |
| Test-selection savings | Execution time/cost avoided through selection versus running everything. |
| Execution duration | Wall-clock duration for equivalent coverage. |
| Worker efficiency | Utilization and throughput of distributed execution. |

### 34.3 Diagnosis

| Metric | Definition |
|---|---|
| Evidence completeness | Share of findings with sufficient evidence to reproduce or explain. |
| Root-cause accuracy | Share of proposed probable causes confirmed by resolution. |
| Time to probable cause | Time from failure detection to a supported root-cause hypothesis. |
| Correlation quality | Precision/recall of grouping related symptoms into the same finding group. |

### 34.4 Reliability of the platform

| Metric | Definition |
|---|---|
| Execution infrastructure failure rate | Runs failing due to platform causes rather than target defects. |
| Flaky test identification | Share of unstable tests correctly identified and explained. |
| Worker recovery success | Share of worker failures recovered without run loss. |

### 34.5 Autonomy

| Metric | Definition |
|---|---|
| Automatically discovered coverage | Coverage achieved through autonomous discovery/probing versus manual specification. |
| Automatically generated useful tests | Generated tests retained and effective over time. |
| Useful autonomous investigation rate | Autonomous investigations producing valid findings or confidence about their absence. |
| Successful self-healing rate | Repairs accepted, surviving, and not causing subsequent instability. |

### 34.6 Release intelligence

| Metric | Definition |
|---|---|
| Quality gate accuracy | Alignment between gate outcomes and actual post-release quality. |
| Release-risk explainability | Share of verdicts whose reasoning users report as sufficient. |
| Regression prevention | Escaped defects that WTE had the evidence to flag but did not. |

> `WTE-PRD-METRIC-001` — WTE must measure itself using these metrics, and must be able to report them per project and per target.

> `WTE-PRD-METRIC-002` — Metrics must never be presented without their definitions, data windows, and confidence.

---

## 35. Product Scope by Horizon

### 35.1 Horizon definitions

| Horizon | Meaning |
|---|---|
| **FOUNDATIONAL** | The primitives everything depends on. No advanced capability is credible without these. |
| **NEAR-TERM** | The first capabilities that make WTE visibly useful for its original audience (web systems). |
| **MID-TERM** | Breadth across major quality dimensions for web and API systems, with intelligence layers maturing. |
| **LONG-TERM** | Platform breadth: infrastructure, data, mobile/desktop, AI systems, specialized domains. |
| **SPECIALIZED / EXTENSION** | Domains and systems representable by the model, delivered through extension mechanisms. |

### 35.2 Foundational layer

The foundation must prioritize reusable primitives:

```
Target          Authorization    Browser        Discovery
Application knowledge            Execution      Capability registry
Evidence        Findings         Testing contracts
Historical runs Quality model    Release model
```

> `WTE-PRD-CORE-028` — No near-term or long-term capability may be delivered by bypassing the foundational primitives; capabilities that cannot use the shared models must be redesigned, not exempted.

### 35.3 Scope summary

| Horizon | Scope summary |
|---|---|
| **FOUNDATIONAL** | One orchestrator; capability registry; target/environment/authorization model; browser execution; web discovery; application knowledge core; execution model with queueing; evidence, finding, history, quality, and release models; reporting basics. |
| **NEAR-TERM** | Broad web-functional testing; visual and accessibility scanning; API (REST) testing; performance measurement and Core Web Vitals; CI/CD gating; change impact and test selection basics; finding correlation within web/API scope. |
| **MID-TERM** | Compatibility matrices; contract/schema testing; authentication/authorization matrices; security baselines (passive); root-cause intelligence across layers; dashboards and integrations; autonomous discovery-to-plan-to-execute within authorization. |
| **LONG-TERM** | Infrastructure, cloud, Kubernetes, data, mobile, desktop, reliability/chaos/DR, observability/SLO, distributed systems, AI/ML/LLM/RAG/agent evaluation, active security testing under authorization. |
| **SPECIALIZED / EXTENSION** | Vision, audio, video, WebRTC, IoT/embedded, telecom, safety-critical and future domains through the extension model. |

> `WTE-PRD-CORE-029` — Sequencing, dependencies, and phase composition are owned by `PHASES.md`. This PRD defines the destination and the dependency direction, not the schedule.

### 35.4 Why the foundation dominates

Every domain in §13 consumes the same primitives. A visual testing capability that invents its own evidence model, an API capability that invents its own finding model, or a mobile capability that bypasses authorization all reintroduce the fragmentation WTE exists to eliminate.

> `WTE-PRD-CORE-030` — Breadth must never be purchased at the cost of the shared models. A narrower platform with unified models is preferable to a broad platform with silos.

---

## 36. Product Boundaries

WTE is one part of a larger system of responsibilities. Ambiguity about who owns what produces either duplicated effort or unowned risk. The three-way separation below is permanent.

### 36.1 WTE responsibility

WTE owns, for every capability it exposes:

```
Authorization      Scope             Tool selection    Execution policy
Normalization      Evidence          Findings          Correlation
History            Root cause        Quality           Release readiness
Reporting          Audit             Learning
```

> `WTE-PRD-CORE-049` — WTE must always remain responsible for authorization, scope enforcement, tool/capability selection, execution policy, normalization, evidence integrity, findings, correlation, history, quality, reporting, and audit — even when the actual testing mechanics are performed by an external engine or tool.

### 36.2 External engine / tool responsibility

An external engine, scanner, framework, or service is responsible for the specialized mechanics it is built for: scanning algorithms, protocol implementations, load generation, model evaluation harnesses, and similar domain machinery.

External engines:

- do not own authorization decisions;
- do not define scope;
- do not control what WTE stores as evidence or how it is classified;
- do not decide whether a release is ready;
- and must not become a requirement of the product (§18.2, `WTE-PRD-ORCH-002`).

> `WTE-PRD-CORE-050` — An external engine may be replaced at any time without changing WTE's models, history, or conclusions. If a tool change destroys history or invalidates comparisons, the integration is defective.

### 36.3 User / organization responsibility

The user and their organization own:

```
Target ownership and authority to test
Scope definitions and criticality declarations
Environment provisioning and credentials
Policies, release gates, and mandates
Risk acceptance, waivers, and exceptions
Remediation decisions and timelines
Legal and regulatory conclusions (including compliance determinations)
Data governance for their own systems and data
```

> `WTE-PRD-CORE-051` — WTE must not assume organizational responsibilities: it produces evidence and assessments, and must ask the organization to make decisions that belong to the organization.

### 36.4 Responsibility map for common activities

| Activity | WTE | External engine/tool | Organization |
|---|---|---|---|
| Authorization | Grants, enforces, audits | Must obey | Defines who may authorize and under what policy |
| Scope | Enforces at request level | Must obey | Declares scope and ownership |
| Specialized test mechanics | Selects, configures, invokes, interprets | Executes | Provides environment and access |
| Evidence | Captures, normalizes, classifies, retains | Provides raw output | Sets retention and privacy policy |
| Findings | Creates, deduplicates, correlates, tracks | May provide raw candidate signals | Triage, remediation decisions |
| Root cause | Correlates and hypothesizes with confidence | May supply specialized diagnostics | Confirms and fixes |
| Quality assessment | Computes and explains | — | Chooses policy and thresholds |
| Release readiness | Assesses and explains | — | Decides to release, accepts risk |
| Compliance | Produces technical evidence | May contribute specialized reports | Makes legal/regulatory determinations |

> `WTE-PRD-CORE-052` — Responsibility boundaries must be visible in the product: a user must always be able to determine which party performed which part of an activity and which conclusions WTE itself stands behind.

---

## 37. Product Constraints

Constraints are conditions the product must operate within. They are not negotiable by feature request.

### 37.1 Safety and authorization constraints

> `WTE-PRD-CORE-031` — WTE must not be capable of executing any operation outside an explicit, valid, in-scope authorization, regardless of who or what requests it.

> `WTE-PRD-CORE-032` — WTE must be safe by default: the least-invasive capable behavior is the default for every capability, every target, and every new user.

> `WTE-PRD-CORE-033` — WTE must never perform destructive operations as part of autonomous behavior.

### 37.2 Epistemic constraints

> `WTE-PRD-CORE-034` — WTE must never assert a conclusion its evidence does not support, and must represent unknown, untested, and uncertain states explicitly.

> `WTE-PRD-CORE-035` — WTE must never fabricate results, evidence, coverage, or confidence — including under partial failure, missing data, or unavailable engines.

> `WTE-PRD-CORE-036` — WTE must never conflate observation with judgment, or correlation with causation, in its data model, interfaces, or reports.

### 37.3 Self-assessment constraints

> `WTE-PRD-CORE-037` — WTE must not certify itself: it must not declare its own capabilities verified without external verification evidence.

> `WTE-PRD-CORE-038` — WTE must not certify the systems it tests: it produces evidence and assessments, not certifications or regulatory approvals.

### 37.4 Architecture-level constraints (product-visible)

> `WTE-PRD-CORE-039` — WTE must remain vendor-independent: no core product capability may require a single external tool.

> `WTE-PRD-CORE-040` — WTE must remain deployable in restricted environments, including those with limited egress, private networks, and air-gapped operation.

> `WTE-PRD-CORE-041` — WTE must keep evidence and knowledge exportable: customers must never be locked out of their own quality data.

> `WTE-PRD-CORE-042` — WTE must not require customers to hand over source code or production data to obtain value; testing must be possible from the outside.

### 37.5 Economic constraints

> `WTE-PRD-CORE-043` — WTE must make execution and AI costs attributable and boundable, because untracked cost destroys the trust that autonomy requires.

> `WTE-PRD-CORE-044` — WTE must scale down as well as up: it must be usable by an individual developer on a laptop and by an enterprise cluster, with the same models.

---

## 38. Assumptions

These are assumed true for the product definition. Each must be validated; an invalidated assumption is a product risk (§39) and may require PRD revision.

| ID | Assumption | Impact if invalid |
|---|---|---|
| `A-1` | Users can grant WTE authorized access to a representative environment of each system under test. | Testing scope collapses to what is publicly observable; many capabilities become unavailable. |
| `A-2` | Systems expose observable behavior (DOM, APIs, logs, metrics) that can be captured without modifying the system. | Intelligence quality drops; invasive instrumentation becomes necessary and must be authorized. |
| `A-3` | Test credentials and test data can be provisioned in non-production environments. | Authenticated and state-changing testing becomes impractical. |
| `A-4` | Organizations are willing to define critical workflows, policies, and release gates. | Release readiness reduces to generic defaults and loses organizational meaning. |
| `A-5` | External tools will continue to exist and be integrable rather than being replaced by WTE. | WTE must implement more capability internally, increasing scope and cost. |
| `A-6` | Deterministic oracles (expected values, schemas, invariants) are available for a meaningful portion of behavior; the remainder requires judgment. | Quality assessment becomes more probabilistic and must be presented with lower confidence. |
| `A-7` | Systems under test can be exercised repeatedly and safely within authorized limits. | Discovery, regression, and flakiness intelligence are weakened. |
| `A-8` | Users accept that autonomous behavior is bounded by explicit authorization and prefer it that way. | Autonomy adoption slows; value delivery depends more on assisted modes. |
| `A-9` | Evidence volume can be managed through retention, sampling, and tiered storage. | Storage costs and report usability degrade. |
| `A-10` | Modern AI models are useful for correlation and reasoning but not reliable enough to be the sole source of a quality decision. | Design assumption of AI-as-layer over evidence is confirmed, not invalidated; the constraint remains. |

> `WTE-PRD-CORE-045` — WTE must detect and surface conditions that indicate an assumption no longer holds (for example: repeatedly missing credentials, absent test data, or authorization refusals), rather than silently degrading.

---

## 39. Risks

### 39.1 Product risks

| ID | Risk | Impact | Mitigation direction |
|---|---|---|---|
| `R-1` | **Scope explosion.** The universal taxonomy tempts implementation of hundreds of shallow capabilities. | Thin, unreliable platform; abandoned foundations. | Enforce `NG-11`, the concept hierarchy, and horizon discipline; breadth only through the shared models. |
| `R-2` | **Fragmentation by acquisition.** Each new domain ships its own models (evidence, findings, reporting). | The exact problem WTE exists to solve returns inside the product. | `WTE-PRD-CORE-002`, `WTE-PRD-CORE-027`, `WTE-PRD-CORE-030`. |
| `R-3` | **False confidence.** Aggregate scores and verdicts imply certainty the evidence does not support. | Users trust the platform, then get burned; trust collapses. | `WTE-PRD-QUAL-005`, `WTE-PRD-QUAL-008`, `WTE-PRD-REL-001`, `WTE-PRD-REL-008`. |
| `R-4` | **Noise.** Findings accumulate faster than they are resolved; users stop reading. | Platform value inverts into burden. | Correlation (§21), deduplication, flakiness intelligence (§24), suppression discipline. |
| `R-5` | **AI overreach.** AI-generated conclusions presented with authority they do not have. | Wrong decisions, eroded trust, safety incidents. | `WTE-PRD-AI-008`–`WTE-PRD-AI-010`, grounding requirements, disclosure. |
| `R-6` | **Prompt injection via targets.** Browsed content manipulates the agent. | Unauthorized actions, secret exposure. | §26.4, platform-side permission enforcement, injection findings. |
| `R-7` | **Authorization model complexity.** Users find authorization obstructive and disable it. | Safety controls bypassed organizationally. | Progressive disclosure, sensible defaults, visible effective authorization, low-friction paths for safe classes. |
| `R-8` | **Autonomy trust gap.** Autonomous execution produces an incident or a costly run. | Autonomy program halted; product value drops. | Laddered autonomy, blast-radius controls, budget caps, kill switch, near-miss reporting. |
| `R-9` | **Vendor dependency drift.** A critical engine's vendor changes licensing, capability, or availability. | Platform capability lost or costs change abruptly. | Multi-engine per capability (`WTE-PRD-ORCH-002`), adapters, health monitoring. |
| `R-10` | **Evidence cost.** Screenshots, video, traces, and HAR files grow unbounded. | Storage/opcosts, slow reports. | Retention classes, sampling, tiered storage, summaries with drilldown. |
| `R-11` | **Score gaming.** Teams optimize the score rather than quality. | Metric becomes a target; quality stagnates. | Explainability, coverage honesty, trend comparisons, multiple dimensions. |
| `R-12` | **Machine-learning of knowledge decays.** Application knowledge becomes stale after rapid change. | Wrong impact analysis and selection. | Knowledge decay (`WTE-PRD-KNOW-011`), staleness marking, discovery refresh. |
| `R-13` | **Platform reliability.** WTE's own failures are interpreted as target defects. | Wrong findings, wasted investigation. | `WTE-PRD-EVID-008`, worker failure modeling, platform metrics (§34.4). |
| `R-14` | **Adoption friction.** Teams cannot justify the setup cost versus existing tools. | No usage; no learning. | Time to first value (`WTE-PRD-NFR-018`), progressive disclosure, standalone value without integrations. |
| `R-15` | **Legal/ethical misuse.** Users attempt unauthorized testing of systems they do not own. | Harm to third parties; platform credibility. | §27.5, authorization verification, refusal and near-miss reporting. |

### 39.2 Risk management principle

> `WTE-PRD-CORE-046` — Product risks must be reviewed as the product evolves; risks that materialize must produce explicit PRD revisions, not silent scope adjustments.

---

## 40. Open Questions

These are genuine, unresolved product decisions. They must not be silently resolved by implementation. Each has an owning document for resolution.

| ID | Open question | Owning document |
|---|---|---|
| `OQ-001` | **Product naming.** WTE is retained for continuity, but the product class is universal. Should the product present a universal name while keeping WTE as the project name, and when? | PRD (product decision) |
| `OQ-002` | **Deployment modes.** Which deployment modes are first-class in the foundation: local developer tool, self-hosted service, cloud service, or all three from the start? | `DEPLOYMENT.md` |
| `OQ-003` | **Multi-tenancy default.** Is the default deployment model single-tenant, or multi-tenant with strong isolation? This affects every model (`WTE-PRD-KNOW-006`, `WTE-PRD-NFR-005`). | `ARCHITECTURE.md`, `SECURITY.md` |
| `OQ-004` | **Evidence retention defaults.** What is the default retention per evidence class, and what must be configurable versus fixed by policy? | `DATABASE.md`, `SECURITY.md` |
| `OQ-005` | **First browser engine(s).** Which browser automation engine(s) constitute the initial foundational set, and what is the minimum viable abstraction over them? | `ARCHITECTURE.md` |
| `OQ-006` | **Test authoring model.** Does WTE expose its own test-definition format/DSL, or does it operate purely on plans, discovered structure, and imported tests? | `ARCHITECTURE.md`, `API.md` |
| `OQ-007` | **Default quality aggregation.** Does WTE ship a default aggregate quality score, or only dimensional scores with an explicit user-defined aggregate? (A default risks false confidence; no default risks unpublishable verdicts.) | PRD + `DESIGN.md` |
| `OQ-008` | **Release verdict default policy.** What is the default gate policy before organizations configure their own, and does it include an `INSUFFICIENT EVIDENCE` state as a first-class outcome? | PRD + `PHASES.md` |
| `OQ-009` | **Manual and exploratory testing scope.** Are manual/exploratory sessions first-class in the near-term, or deferred behind automation? | `PHASES.md` |
| `OQ-010` | **Autonomy default level.** Which autonomy stage is the default for a new target, and what is the minimum human involvement for `MUTATING` classes? | `SECURITY.md`, `DESIGN.md` |
| `OQ-011` | **Browser grid ownership.** Does WTE host execution infrastructure (browser grid, device farm) or integrate with user-provided infrastructure? This affects mobile, cross-browser, and load testing economics. | `ARCHITECTURE.md`, `DEPLOYMENT.md` |
| `OQ-012` | **Compliance framework mapping.** Which technical control frameworks are mapped first for compliance-evidence reporting, and who owns the mappings? | PRD + `SECURITY.md` |
| `OQ-013` | **Monitoring boundary.** Where exactly is the boundary between WTE's synthetic monitoring and a dedicated monitoring/APM system, and what data flows each way? | PRD + `ARCHITECTURE.md` |
| `OQ-014` | **Load-test cost governance.** How are load-generating runs budgeted, priced, and approved, given they consume infrastructure at scale? | `SECURITY.md`, `DEPLOYMENT.md` |
| `OQ-015` | **Extension packaging.** Do extensions have a formal packaging/distribution mechanism (registry, marketplace, signing), and what trust model applies to third-party extensions? | `ARCHITECTURE.md`, `SECURITY.md` |
| `OQ-016` | **Data residency.** How is regional data residency handled for evidence, knowledge, and AI processing? | `DEPLOYMENT.md`, `SECURITY.md` |
| `OQ-017` | **AI model strategy.** Which AI capabilities are required for the near-term intelligence layer, and how is model portability maintained given rapid ecosystem change? | `ARCHITECTURE.md` |
| `OQ-018` | **Mobile device strategy.** Real-device cloud, local emulators/simulators, or both — and which is required for credible mobile performance results? | `ARCHITECTURE.md`, `PHASES.md` |
| `OQ-019` | **Self-healing default policy.** Is self-healing proposed-only, approval-required, or auto-accepted by default? | `SECURITY.md`, `DESIGN.md` |
| `OQ-020` | **Certification boundary for regulated domains.** What precisely may WTE claim for safety-critical and regulated domains (evidence generation only, process attestation, none), and how is this enforced in reporting? | `SECURITY.md`, PRD |
| `OQ-021` | **Historical baseline governance.** Who owns approving baseline changes, and what prevents baseline drift from masking regressions? | `DESIGN.md`, `PHASES.md` |
| `OQ-022` | **Sibling document ownership.** When are `ARCHITECTURE.md`, `RULES.md`, `DESIGN.md`, and `PHASES.md` authored, and which one is authoritative when this PRD and a sibling document disagree? | Repository governance |

> `WTE-PRD-CORE-047` — Unresolved open questions must be resolved explicitly and recorded; they must never be resolved implicitly by implementation choices that contradict this document.

---

## 41. Definition of Product Success

### 41.1 The North-Star principle

> **WTE does not exist to run the greatest number of tests.** It exists to create the most complete, trustworthy, evidence-driven understanding of software quality and release risk possible, while safely selecting and coordinating the right testing capabilities for each system.

And:

> **WTE should eventually be able to look at an authorized software system, understand what it is, understand how it works, understand what can fail, determine how those risks should be tested, execute the appropriate testing safely, collect evidence, diagnose failures, and explain whether that system is ready to release.**

### 41.2 What success looks like

WTE has succeeded when:

1. **A user can point WTE at an authorized system and receive understanding** — structure, dependencies, workflows, and risks — without having enumerated them manually.
2. **Testing is proportionate to risk.** Selection is explainable; coverage consequences are visible; mandated gates are never silently reduced.
3. **Failures arrive explained.** Symptoms are correlated, findings deduplicated, probable causes proposed with confidence, and next actions recommended.
4. **Quality is measurable and explainable.** Every dimension, score, and verdict decomposes into findings, evidence, and policy — with coverage honesty.
5. **Release decisions are defensible.** READY / CONDITIONALLY READY / NOT READY outcomes cite specific evidence, and remain reproducible after the fact.
6. **The platform compounds.** History makes testing cheaper, sharper, and more predictive with every run.
7. **The platform is safe.** No operation exceeds authorization; powerful capabilities are bounded, auditable, abortable, and reversible.
8. **The platform is honest.** Untested areas are reported as untested; AI conclusions are labeled; nothing is fabricated.
9. **The platform is open.** New domains, capabilities, engines, and integrations are added without redesign or vendor lock-in.
10. **The platform is trusted infrastructure.** Teams rely on it the way they rely on source control and CI — as a durable part of how software quality is practiced.

### 41.3 PRD completion gate

This document is complete only if it answers the following questions coherently. Each is answered in the cited section.

| Question | Where answered |
|---|---|
| What is WTE? | §4.1–§4.6 |
| Why does WTE exist? | §3, §5 |
| Who uses it? | §9, §10 |
| What systems can it ultimately test? | §11 |
| What types of software testing must it understand? | §13 |
| How are testing categories normalized into capabilities? | §13.1–§13.2, §13.39 |
| How does it remain vendor-independent? | §4.5, §18.2, §32.2, `WTE-PRD-ORCH-002` |
| How does discovery lead to intelligent testing? | §13.6, §15, §16, §17 |
| How does Application Knowledge improve testing? | §13.7, §14 |
| How are tools selected? | §18.1–§18.2 |
| How is execution authorized? | §27 |
| How is evidence collected? | §19 |
| How do observations become findings? | §20.1–§20.2 |
| How are related failures correlated? | §21 |
| How is root cause determined? | §22 |
| How does history improve future testing? | §23 |
| How are tests generated? | §15 |
| How are relevant tests selected? | §17 |
| How are flaky tests identified? | §24 |
| How can automation self-heal safely? | §25 |
| How does AI participate without replacing evidence? | §26.1 |
| How is quality measured? | §28 |
| How is release readiness decided? | §29 |
| How can future testing domains be added? | §13.38, `WTE-PRD-EXT-001` |
| What is current versus future? | §1.3–§1.4, §13.40, §35 |
| What is explicitly outside WTE's responsibility? | §8, §13.38 (`WTE-PRD-EXT-004`), §36, §37 |

### 41.4 Closing statement

Software quality is not a tool problem; it is an understanding problem. Tools produce observations. Understanding requires structure, evidence, correlation, history, and judgment applied at the right moment.

WTE exists to make that understanding reliable, explainable, and safe — for websites today, for software systems generally over time, and always within the boundaries its users explicitly authorize.

---

## Annex A — Universal Taxonomy Coverage Map

This annex maps the universal testing taxonomy to the sections of this PRD where each domain is defined, so that coverage is verifiable rather than asserted.

| Domain | PRD coverage | Horizon |
|---|---|---|
| Testing foundations (static/dynamic, box models, specification/structure/experience, manual/automated/exploratory, positive/negative, risk/change-based, model/property/metamorphic/differential, boundary/equivalence/decision-table/state-transition/pairwise/combinatorial) | §13.3.1 | FOUNDATIONAL |
| Release & change testing (smoke, sanity, regression, selective regression, confirmation, release, production verification, canary, post-deployment) | §13.3.2 | FOUNDATIONAL → PLANNED |
| Test levels (unit, component, integration, system, E2E, acceptance, UAT, OAT, alpha, beta, field) | §13.4 | FOUNDATIONAL → PLANNED |
| Target & environment (identity, reachability, localhost/LAN, dev/test/staging/prod, comparison, drift, proxy, routing, DNS overrides, secret references, scope, authorization boundaries) | §13.5 | FOUNDATIONAL |
| Discovery & reconnaissance (sites, pages, routes, hidden routes, navigation, links, forms, inputs, buttons, assets, media, iframes, Shadow DOM, Web Components, service workers, PWA manifests, APIs, GraphQL, WebSockets, SSE, third parties, analytics, tracking, technology stack, authentication systems) | §13.6 | FOUNDATIONAL (web) → PLANNED |
| Application knowledge (applications, pages, routes, components, APIs, services, workflows, roles, permissions, dependencies, databases, infrastructure, third parties, tests, coverage, findings, changes, failures, releases + relationships) | §13.7, §14 | FOUNDATIONAL |
| Browser automation (lifecycle, navigation, interaction, mouse/keyboard/touch, forms, files, downloads/uploads, clipboard, permissions, popups, dialogs, frames, tabs/windows, storage, cookies, contexts, geolocation, camera, microphone, notifications, device emulation) | §13.8 | FOUNDATIONAL |
| Functional testing (navigation, links, menus, buttons, forms, validation, CRUD, search, filtering, sorting, pagination, infinite scroll, uploads/downloads, tables, data grids, charts, dashboards, wizards, steppers, modals, drawers, notifications, toasts, shortcuts, state, sessions, refresh, deep links, recovery) | §13.9.1 | FOUNDATIONAL → PLANNED |
| Business logic testing (rules, eligibility, pricing, discounts, limits, approvals, transitions, calculations, entitlements, billing, subscriptions, inventory, invariants) | §13.9.2 | PLANNED |
| User journey & workflow testing (critical journeys, cross-page, cross-service, business processes, long-running, recovery, compensation, partial completion, interruption) | §13.9.3 | FOUNDATIONAL → PLANNED |
| UI testing (rendering, components, states, layout, alignment, spacing, typography, color, icons, images, z-index, visibility, overflow, collision, clipping, responsive states, loading/empty/error/disabled/focus/hover states) | §13.10 | PLANNED |
| UX testing (usability, discoverability, clarity, feedback, consistency, affordance, cognitive load, friction, error prevention/recovery, navigation clarity, task completion, touch ergonomics, readability, hierarchy) | §13.11 | PLANNED → LONG-TERM |
| Visual testing (screenshots, pixel/structural comparison, baselines, visual regression, component/page/responsive/cross-browser/theming, anomaly detection) | §13.12 | PLANNED |
| Accessibility (WCAG, ARIA, semantic HTML, names, keyboard, focus, contrast, alt text, landmarks, headings, forms, tables, live regions, accessibility tree, screen readers, assistive technologies) | §13.13 | PLANNED → LONG-TERM |
| Responsive & device testing (desktop, laptop, tablet, mobile, foldable, orientation, DPR, touch, breakpoints, adaptive navigation, overflow, collision, clipping, responsive images/typography) | §13.14 | PLANNED |
| Cross-browser & compatibility (Chrome/Chromium, Edge, Firefox, Safari/WebKit, mobile browsers, versions, OS, devices, runtimes, databases, APIs, dependencies, backward/forward compatibility, interoperability, conformance) | §13.14 | PLANNED |
| API testing — REST & HTTP (methods, headers, cookies, auth, payloads, schema, pagination, filtering, sorting, rate limits, retries, idempotency, errors, versioning) | §13.15.1 | PLANNED |
| GraphQL (queries, mutations, subscriptions, schema, resolvers, variables, fragments, pagination, authorization, complexity, errors) | §13.15.2 | LONG-TERM |
| gRPC (unary, streaming, protobuf, metadata, auth, status codes, interoperability, compatibility) | §13.15.3 | LONG-TERM |
| SOAP/XML (WSDL, envelopes, schemas, WS-Security, auth, faults, interoperability) | §13.15.4 | LONG-TERM |
| Realtime protocols (WebSockets, SSE, WebRTC, streaming, reconnect, ordering, duplicates, latency, realtime authorization) | §13.15.5 | LONG-TERM |
| Messaging & event systems (Kafka, RabbitMQ/AMQP, MQTT, NATS, Redis Streams, SQS, SNS, Pub/Sub, Service Bus; producers, consumers, schemas, ordering, retries, DLQs, eventual consistency) | §13.15.6 | LONG-TERM |
| Contract & schema testing (API contracts, consumer-driven contracts, OpenAPI, JSON Schema, GraphQL schema, XML Schema, protobuf, database schema, compatibility, breaking-change detection) | §13.15.7 | PLANNED |
| Mocking & service virtualization (mocks, stubs, fakes, virtualization, dependency simulation, fault simulation, deterministic environments) | §13.15.8 | PLANNED |
| Authentication (login, logout, registration, reset, verification, OTP, TOTP, SMS/email OTP, MFA, passkeys/WebAuthn, SSO, OAuth, OIDC, SAML, LDAP, AD, social, magic links, remember me, device trust, token refresh/rotation) | §13.16.1 | PLANNED → LONG-TERM |
| Authorization & identity (RBAC, ABAC, ReBAC, PBAC, object/function/field/row authorization, tenant isolation, inheritance, explicit deny, escalation, direct-route authz, API authz, UI authz, provisioning, identity lifecycle) | §13.16.2 | PLANNED → LONG-TERM |
| Session security (creation, expiry, fixation, logout invalidation, token expiry/rotation, cookie protection, concurrent sessions, device sessions) | §13.16.3 | PLANNED |
| Security testing (information gathering, configuration, identity, authentication, authorization, session, input validation, injection, cryptography, business-logic security, client-side, API security, HTTP security, threat validation, abuse cases) | §13.17.1 | PLANNED → LONG-TERM |
| Application security technologies (SAST, DAST, IAST, RASP validation, SCA, dependency analysis, secret scanning, SBOM, supply chain, fuzzing, pentest support, security regression) | §13.17.2 | LONG-TERM |
| Cryptography & TLS (certificates, chains, expiry, hostname validation, TLS versions, ciphers, HSTS, OCSP, key handling, randomness, configuration) | §13.18.1 | PLANNED |
| HTTP security (CSP, CORS, HSTS, clickjacking, Referrer-Policy, Permissions-Policy, mixed content, cache security, cookie attributes, headers) | §13.18.2 | PLANNED |
| Privacy (consent, cookies, tracking, PII leakage, minimization, retention, deletion, export, controls, sensitive evidence) | §13.19 | LONG-TERM |
| Network (connectivity, routing, latency, loss, bandwidth, ports, protocols, proxies, capture, errors, degradation) | §13.22 | LONG-TERM |
| DNS (A, AAAA, CNAME, MX, TXT, NS, CAA, DNSSEC, TTL, propagation, failover) | §13.22 | LONG-TERM |
| CDN & edge (caching, routing, edge functions, geographic delivery, invalidation, headers, failover) | §13.22 | LONG-TERM |
| Performance (page, API, backend, frontend, rendering, CPU, memory, resources, navigation/resource timing, long tasks, layout shifts, regression, budgets) | §13.20 | PLANNED → LONG-TERM |
| Core Web Vitals (LCP, INP, CLS, FCP, TTFB, long animation frames, navigation/resource timing) | §13.20.1 | PLANNED |
| Load & scalability (smoke, average, load, stress, spike, soak/endurance, volume, concurrency, capacity, breakpoint, scalability, distributed load) | §13.21 | LONG-TERM |
| Resource/runtime testing (CPU, memory, heap, GC, threads, processes, sockets, file descriptors, pools, disk, quotas, leaks) | §13.20 | LONG-TERM |
| Database testing (functionality, queries, transactions, constraints, referential integrity, procedures, triggers, indexes, locks, deadlocks, connections, performance) | §13.23 | LONG-TERM |
| Database migration (schema migrations, forward migration, rollback, transformations, backward compatibility, zero-downtime) | §13.23 | LONG-TERM |
| Data quality (accuracy, completeness, consistency, validity, uniqueness, freshness, integrity, reconciliation) | §13.24 | LONG-TERM |
| Data pipelines (ETL, ELT, batch, streaming, transformations, reconciliation, warehouses, analytics) | §13.24 | LONG-TERM |
| BI & analytics (dashboards, metrics, aggregations, filters, drilldowns, exports, charts, business calculations) | §13.24 | LONG-TERM |
| Search systems (indexing, querying, ranking, relevance, filtering, faceting, synonyms, typos, freshness, performance) | §13.24 | LONG-TERM |
| Cache testing (hits, misses, invalidation, expiration, consistency, stale data, fallback, stampedes) | §13.24 | LONG-TERM |
| File & document testing (CSV, XLSX, PDF, JSON, XML, YAML, ZIP, images, documents, encoding, MIME, checksums, corruption, size, metadata) | §13.25 | PLANNED |
| File upload testing (types, MIME validation, size limits, malformed files, security, storage, scanning, duplicates, recovery) | §13.25 | PLANNED |
| Email testing (delivery, SMTP, HTML/plain text, templates, links, OTP, verification, attachments, headers, SPF/DKIM/DMARC, responsive email) | §13.25 | LONG-TERM |
| Notifications (email, SMS, push, web push, Slack, Teams, webhooks, incident notifications) | §13.25 | LONG-TERM |
| Localization & i18n (languages, missing translations, fallback, RTL, Unicode, currency, numbers, dates, times, timezones, calendars, addresses, phones, expansion, truncation) | §13.26 | LONG-TERM |
| Payments (checkout, authorization, capture, failure, retry, refunds, partial refunds, subscriptions, recurring, webhooks, currency, tax) | §13.27 | LONG-TERM |
| E-commerce (catalog, products, variants, pricing, discounts, coupons, cart, wishlist, checkout, shipping, tax, inventory, orders, returns, refunds, subscriptions) | §13.27 | LONG-TERM |
| SEO (titles, meta descriptions, canonicals, robots, sitemaps, Open Graph, social metadata, structured data, hreflang, links, redirects, crawlability, indexability) | §13.28 | PLANNED |
| Content & CMS (presence, duplicates, broken content, publishing, drafts, preview, revisions, permissions, scheduled publishing, workflows) | §13.28 | LONG-TERM |
| PWA & service workers (manifests, installability, offline, caching, lifecycle, updates, background behavior, fallback) | §13.28 | LONG-TERM |
| Mobile (Android, iOS, native, hybrid, webview, mobile browsers, gestures, permissions, orientation, lifecycle, background/foreground, notifications) | §13.29 | LONG-TERM |
| Mobile performance (startup, CPU, memory, battery, network, frames, rendering, storage, app size) | §13.29 | LONG-TERM |
| Desktop (Windows, macOS, Linux, Electron, native, window management, OS integration, file systems, permissions) | §13.30 | LONG-TERM |
| Install / upgrade / uninstall (clean install, prerequisites, upgrade, downgrade, migration, uninstall, residual data, configuration preservation) | §13.30 | LONG-TERM |
| Build testing (dependency install, clean/incremental/production builds, reproducibility, bundle output, artifact integrity) | §13.31 | PLANNED |
| Code quality (formatting, linting, type checking, complexity, dead code, static quality, conventions) | §13.31 | PLANNED |
| Code coverage (line, statement, function, branch, path, requirement, workflow, UI, API) | §13.31 | PLANNED → LONG-TERM |
| Mutation testing (suite defect-detection strength) | §13.31 | LONG-TERM |
| CI/CD (pipelines, builds, tests, gates, artifacts, promotion, rollback, protected environments, release workflows) | §13.31, §12.5 | PLANNED |
| Containers (image builds, startup, health, networking, volumes, secrets, limits, restart, shutdown, security) | §13.32 | LONG-TERM |
| Kubernetes (deployments, statefulsets, services, ingress, policies, health, scaling, scheduling, limits, secrets, configmaps, failures, recovery) | §13.32 | LONG-TERM |
| Infrastructure as code (Terraform, OpenTofu, CloudFormation, Ansible; syntax, config, security, policy, drift, deployment behavior) | §13.32 | LONG-TERM |
| Cloud (AWS, Azure, GCP; identity, networking, storage, compute, policies, config, security, availability, managed services) | §13.32 | LONG-TERM |
| Serverless (functions, events, cold starts, concurrency, timeouts, permissions, retries, dead letters) | §13.32 | LONG-TERM |
| Deployment testing (smoke, health, readiness, liveness, rolling, blue/green, canary, rollback, version/config validation) | §13.31, §13.32 | PLANNED → LONG-TERM |
| Reliability (retries, timeouts, circuit breakers, failover, redundancy, degradation, partial and dependency failures) | §13.33 | LONG-TERM |
| Chaos engineering (network faults, service/worker/database/cache failure, resource pressure, latency, packet loss, infrastructure failure) | §13.33 | LONG-TERM |
| Disaster recovery (backup, restore, PITR, failover, region/database/object storage/config recovery, RTO, RPO) | §13.33 | LONG-TERM |
| Observability (logs, metrics, traces, correlation IDs, telemetry, health, instrumentation, completeness) | §13.34 | PLANNED → LONG-TERM |
| Monitoring (availability, synthetic journeys, API/DNS/TLS monitoring, certificate and domain expiry, alerting) | §13.34 | LONG-TERM |
| SLO/SLA validation (availability, latency, error rates, reliability, error budgets) | §13.34 | LONG-TERM |
| Test data (fixtures, factories, synthetic data, seeds, masking, anonymization, determinism, versioning, lifecycle) | §13.24 | LONG-TERM |
| Configuration & feature flags (matrices, environment variables, flags, gradual rollout, targeting, fallback, kill switches) | §13.35 | PLANNED → LONG-TERM |
| Multi-tenant / SaaS (tenant isolation, configuration, plans, entitlements, billing, metering, performance isolation, data isolation) | §13.35 | LONG-TERM |
| Distributed systems (consensus, partitions, replication, eventual consistency, clocks, retries, duplicates, node failures, leader changes) | §13.36 | LONG-TERM |
| Concurrency (races, threads, locks, async, deadlocks, ordering, synchronization) | §13.36 | LONG-TERM |
| Time & clock (timezones, DST, drift, scheduled jobs, expiry, calendar boundaries, date changes, long-running operations) | §13.36 | LONG-TERM |
| Queues & schedulers (scheduling, priorities, retries, ordering, concurrency, DLQs, delayed jobs, duplicates, recovery) | §13.36 | LONG-TERM |
| Migration (database, cloud, platform, application, legacy, user, data) | §13.23, §13.36 | LONG-TERM |
| Enterprise integration (CRM, ERP, HRIS, identity systems, middleware, document systems, internal services) | §13.36 | LONG-TERM |
| AI/ML model testing (accuracy, precision, recall, F1, calibration, robustness, drift, bias, fairness, latency, throughput, memory, regression) | §13.37.1 | LONG-TERM |
| LLM testing (correctness, relevance, consistency, instruction following, structured/JSON output, hallucination, safety, cost, latency, comparison, prompt regression) | §13.37.2 | LONG-TERM |
| RAG testing (retrieval recall/precision, context relevance/coverage, faithfulness, answer relevance, hallucination, citations, grounding, chunk quality, retriever regression, reranker quality) | §13.37.3 | LONG-TERM |
| AI agent testing (planning, tool selection/arguments/ordering/execution, retry, recovery, memory, context, state, delegation, multi-agent, browser/API actions, goal completion, latency, cost, safety, authorization) | §13.37.4 | LONG-TERM |
| Agent trajectory testing (task → plan → tool choice → tool call → observation → state update → next action → result) | §13.37.5 | LONG-TERM |
| AI safety (prompt injection, indirect injection, jailbreaks, data leakage, tool abuse, unauthorized access, excessive agency, unsafe outputs, exfiltration, policy violations) | §13.37.6, §26.4 | LONG-TERM |
| AI reliability (run variance, model variability, tool failures, recovery, context loss, memory errors, loops, non-termination, cost overruns) | §13.37.7 | LONG-TERM |
| AI grounding (hallucination, citation accuracy, attribution, evidence grounding, unsupported claims) | §13.37.8 | LONG-TERM |
| Computer vision (image understanding, detection, OCR, visual localization, layout understanding, anomaly detection) | §13.38 | EXTENSION |
| Audio & voice (ASR, TTS, audio quality, pronunciation, latency, languages, streaming audio) | §13.38 | EXTENSION |
| Video & streaming (playback, streaming, buffering, codecs, adaptive bitrate, synchronization, captions, DRM, quality) | §13.38 | EXTENSION |
| WebRTC & communication (signaling, audio, video, NAT traversal, reconnect, latency, packet loss, media quality) | §13.38, §13.15.5 | EXTENSION |
| IoT, embedded & firmware (devices, firmware, hardware/software integration, device-cloud communication, updates, connectivity, telemetry) | §13.38 | EXTENSION |
| Protocol & telecom (conformance, interoperability, telecom systems, network appliances, 4G/5G, specialized transports) | §13.38 | EXTENSION |
| Safety-critical systems (automotive, medical, industrial, aviation, robotics) | §13.38 | EXTENSION |
| Test management (cases, suites, plans, runs, traceability, coverage, assignments, history, status) | §18.6 | PLANNED |
| Defect & finding management (findings, dedup, status, severity, ownership, history, issue integration, regression, resolution, reopening) | §20 | FOUNDATIONAL |
| Evidence management (screenshots, video, DOM, accessibility trees, HAR, traces, console, network, API responses, metrics, logs, distributed traces, database output, files, artifacts) | §19 | FOUNDATIONAL |
| Root-cause analysis (correlation across browser/network/API/database/log/metric/trace/change/deployment/failure/dependency data) | §22 | PLANNED → LONG-TERM |
| Change impact analysis (diffs, AST, dependency/route/API/component/workflow graphs, coverage, history) | §16 | PLANNED |
| Intelligent test selection (risk, change, criticality, history, coverage, dependencies, flakiness, cost, release scope) | §17 | PLANNED |
| Test generation (discovery, DOM, accessibility tree, graphs, OpenAPI, GraphQL, schemas, source, requirements, stories, existing tests, historical failures, telemetry) | §15 | PLANNED → LONG-TERM |
| Flaky test intelligence (history, timing, environment, browser, network, selectors, duration, clustering, score) | §24 | PLANNED |
| Self-healing (selectors, locators, text, role, visual locators, timing, waits — audited, versioned, confidence-scored, reversible, re-tested) | §25 | LONG-TERM |
| Continuous & autonomous testing (scheduled, CI, deployment, continuous verification, monitoring, autonomous discovery/planning/selection/execution/correlation/investigation) | §12.5, §12.6, §26 | PLANNED → LONG-TERM |
| Testing the testing platform (engines, adapters, rules, evaluators, registry, orchestrator, workers, evidence, findings, AI decisions, scores, release decisions) | §18.7 | FOUNDATIONAL |

---


---

## Annex B — Product Requirement Index

Stable identifiers defined in this document. IDs are never reused or renumbered (§1.6) and may appear as cross-references elsewhere.

| Prefix | Area | Count | Range |
|---|---|---|---|
| `WTE-PRD-CORE` | Platform fundamentals and product model | 52 | `CORE-001 … CORE-052` |
| `WTE-PRD-TARGET` | Targets and environments | 10 | `TARGET-001 … TARGET-010` |
| `WTE-PRD-AUTH` | Authorization and safe execution | 30 | `AUTH-001 … AUTH-030` |
| `WTE-PRD-DISC` | Discovery and reconnaissance | 6 | `DISC-001 … DISC-006` |
| `WTE-PRD-KNOW` | Application knowledge | 16 | `KNOW-001 … KNOW-016` |
| `WTE-PRD-BROWSER` | Browser automation | 6 | `BROWSER-001 … BROWSER-006` |
| `WTE-PRD-FUNC` | Functional and business logic | 7 | `FUNC-001 … FUNC-007` |
| `WTE-PRD-UIUX` | UI and UX | 8 | `UIUX-001 … UIUX-008` |
| `WTE-PRD-VISUAL` | Visual and computer vision | 5 | `VISUAL-001 … VISUAL-005` |
| `WTE-PRD-COMPAT` | Responsive and compatibility | 4 | `COMPAT-001 … COMPAT-004` |
| `WTE-PRD-API` | APIs, protocols, and contracts | 6 | `API-001 … API-006` |
| `WTE-PRD-IDENT` | Authentication, authorization, session | 6 | `IDENT-001 … IDENT-006` |
| `WTE-PRD-SEC` | Security testing and application security | 8 | `SEC-001 … SEC-008` |
| `WTE-PRD-PRIV` | Privacy | 4 | `PRIV-001 … PRIV-004` |
| `WTE-PRD-PERF` | Performance | 6 | `PERF-001 … PERF-006` |
| `WTE-PRD-LOAD` | Load and scalability | 5 | `LOAD-001 … LOAD-005` |
| `WTE-PRD-NET` | Network, DNS, TLS, edge | 6 | `NET-001 … NET-006` |
| `WTE-PRD-DB` | Database | 4 | `DB-001 … DB-004` |
| `WTE-PRD-DATA` | Data quality and pipelines | 6 | `DATA-001 … DATA-006` |
| `WTE-PRD-MSG` | Email and notifications | 3 | `MSG-001 … MSG-003` |
| `WTE-PRD-PAY` | Payments | 3 | `PAY-001 … PAY-003` |
| `WTE-PRD-ECOM` | E-commerce | 1 | `ECOM-001 … ECOM-001` |
| `WTE-PRD-SEO` | SEO and content | 3 | `SEO-001 … SEO-003` |
| `WTE-PRD-PWA` | PWA and service workers | 1 | `PWA-001 … PWA-001` |
| `WTE-PRD-MOBILE` | Mobile | 3 | `MOBILE-001 … MOBILE-003` |
| `WTE-PRD-DESKTOP` | Desktop | 2 | `DESKTOP-001 … DESKTOP-002` |
| `WTE-PRD-BUILD` | Build and code quality | 3 | `BUILD-001 … BUILD-003` |
| `WTE-PRD-CICD` | CI/CD | 3 | `CICD-001 … CICD-003` |
| `WTE-PRD-INFRA` | Containers, Kubernetes, IaC | 4 | `INFRA-001 … INFRA-004` |
| `WTE-PRD-CLOUD` | Cloud and serverless | 2 | `CLOUD-001 … CLOUD-002` |
| `WTE-PRD-RELIAB` | Reliability engineering | 1 | `RELIAB-001 … RELIAB-001` |
| `WTE-PRD-CHAOS` | Chaos engineering | 2 | `CHAOS-001 … CHAOS-002` |
| `WTE-PRD-DR` | Disaster recovery | 2 | `DR-001 … DR-002` |
| `WTE-PRD-OBS` | Observability and monitoring | 3 | `OBS-001 … OBS-003` |
| `WTE-PRD-SLO` | SLO/SLA validation | 1 | `SLO-001 … SLO-001` |
| `WTE-PRD-AI` | AI, ML, LLM, RAG, agents | 28 | `AI-001 … AI-028` |
| `WTE-PRD-EVID` | Evidence | 10 | `EVID-001 … EVID-010` |
| `WTE-PRD-FIND` | Findings | 10 | `FIND-001 … FIND-010` |
| `WTE-PRD-CORR` | Correlation | 8 | `CORR-001 … CORR-008` |
| `WTE-PRD-RCA` | Root-cause intelligence | 7 | `RCA-001 … RCA-007` |
| `WTE-PRD-HIST` | Historical intelligence | 7 | `HIST-001 … HIST-007` |
| `WTE-PRD-IMPACT` | Change impact analysis | 7 | `IMPACT-001 … IMPACT-007` |
| `WTE-PRD-SELECT` | Intelligent test selection | 8 | `SELECT-001 … SELECT-008` |
| `WTE-PRD-GEN` | Test generation | 8 | `GEN-001 … GEN-008` |
| `WTE-PRD-FLAKY` | Flaky test intelligence | 7 | `FLAKY-001 … FLAKY-007` |
| `WTE-PRD-HEAL` | Self-healing | 7 | `HEAL-001 … HEAL-007` |
| `WTE-PRD-QUAL` | Quality model | 10 | `QUAL-001 … QUAL-010` |
| `WTE-PRD-REL` | Release readiness | 9 | `REL-001 … REL-009` |
| `WTE-PRD-REPORT` | Reporting | 9 | `REPORT-001 … REPORT-009` |
| `WTE-PRD-DASH` | Dashboards | 7 | `DASH-001 … DASH-007` |
| `WTE-PRD-INTEG` | Integrations | 7 | `INTEG-001 … INTEG-007` |
| `WTE-PRD-ORCH` | Execution and orchestration | 26 | `ORCH-001 … ORCH-026` |
| `WTE-PRD-NFR` | Non-functional requirements | 18 | `NFR-001 … NFR-018` |
| `WTE-PRD-METRIC` | Product success metrics | 2 | `METRIC-001 … METRIC-002` |
| `WTE-PRD-EXT` | Extensibility | 4 | `EXT-001 … EXT-004` |
| `WTE-PRD-PLAT` | Testing the testing platform | 5 | `PLAT-001 … PLAT-005` |
| **Total** |  | **436** |  |

> `WTE-PRD-CORE-048` — Requirement identifiers must remain stable across PRD revisions; superseded requirements must be marked, not deleted.

---

## Annex C — Glossary

Canonical terminology for this document and, by extension, for the platform. Where a term appears in sibling documents with a different meaning, this glossary is authoritative until that document explicitly supersedes it.

| Term | Definition |
|---|---|
| **WTE** | Website Testing Engine — the product defined by this document; a universal autonomous software testing and quality intelligence platform. |
| **Target** | An authorized software system (or part of one) that WTE may discover, test, and evaluate. |
| **Environment** | The deployment context in which a target is assessed (local, private, dev, test, staging, production, custom). |
| **Scope** | The declared boundary of what WTE may touch: domains, paths, services, accounts, resources — both included and explicitly excluded. |
| **Authorization** | An explicit grant that permits specified risk classes against a specified target, scope, environment, and time window, attributed to a responsible party. |
| **Risk class** | The classification of an operation by its potential impact: `READ_ONLY`, `SAFE_ACTIVE`, `MUTATING`, `LOAD_GENERATING`, `SECURITY_ACTIVE`, `INFRASTRUCTURE_MUTATING`, `DESTRUCTIVE`. |
| **Testing domain** | A broad area of quality risk the platform understands (e.g. accessibility, performance). |
| **Testing category** | A coherent group of activities within a domain (e.g. automated accessibility scanning). |
| **Capability** | A vendor-independent product operation WTE can plan, authorize, execute, and evaluate (e.g. `accessibility.scan`). |
| **Engine** | A platform component implementing one or more capabilities. |
| **Adapter** | A connector that lets an engine use a specific external tool or service. |
| **Tool** | An external or internal implementation artifact (framework, scanner, runtime) used through an adapter. |
| **Capability registry** | The platform catalogue describing available capabilities, their risk classes, requirements, evidence, evaluators, and available engines. |
| **Observation** | A raw, factual measurement or capture. |
| **Symptom** | An observable deviation with context, not yet judged. |
| **Finding** | A judged, actionable problem statement with severity, evidence, scope, and lifecycle. |
| **Root cause** | The probable underlying defect or condition explaining one or more findings, with confidence and evidence. |
| **Recommendation** | A suggested next action derived from findings and root-cause analysis. |
| **Evidence** | Stored, immutable, normalized proof captured during execution (screenshots, DOM, HAR, traces, logs, metrics, responses, artifacts). |
| **Evidence class** | A category of evidence with its own schema, storage, security classification, and retention policy. |
| **Execution / Run** | A single instance of a plan against a target, environment, and authorization, producing results, evidence, and findings. |
| **Plan** | The declaration of what will be executed for a purpose: target, environment, capability set, tests, and policy. |
| **Application knowledge model** | WTE's persistent, evidence-backed model of a system: entities and relationships across structure, dependencies, workflows, identities, tests, findings, changes, and releases. |
| **Baseline** | An approved reference state (visual, functional, performance, security posture) used for comparison over time. |
| **Correlation** | The process of grouping related symptoms and findings, and identifying probable shared causes. |
| **Quality dimension** | One axis of quality assessment (functional, accessibility, performance, security, and so on). |
| **Release readiness** | The evidence-backed assessment of whether a release candidate should proceed: READY, CONDITIONALLY READY, or NOT READY. |
| **Quality gate** | A policy-defined checkpoint that can pass, warn, or block promotion based on evidence. |
| **Autonomy** | The degree to which WTE discovers, plans, executes, and investigates without human initiation, bounded by authorization and policy. |
| **Untrusted content** | Any data obtained from a target or external system; never instructions, never a source of permission. |
| **Horizon** | The classification of a capability's maturity commitment: FOUNDATIONAL, PLANNED, LONG-TERM, EXTENSION (with CURRENT meaning verified as implemented). |

---

## Annex D — Document Control

### D.1 Revision history

| Version | Date | Change |
|---|---|---|
| 1.0.0 | 2026-10-04 | Initial authoritative PRD. Authored against a repository containing only `LICENSE`; no sibling documents existed. All capabilities recorded as FOUNDATIONAL/PLANNED/LONG-TERM/EXTENSION; nothing marked CURRENT. |

### D.2 Reviews performed at authoring time

| Review | Result |
|---|---|
| Repository inspection | Repository contained only `LICENSE` (initial commit). No `/docs/PRD.md`, `ARCHITECTURE.md`, `RULES.md`, `DESIGN.md`, `PHASES.md`, `DATABASE.md`, `API.md`, `SECURITY.md`, `TESTING.md`, `DEPLOYMENT.md`, `CHANGELOG.md`, and no application directories. No prior product concepts, terminology, engines, or shared systems existed to preserve. |
| Contradiction audit against sibling documents | Not applicable — sibling documents do not exist yet. The contradiction audit must be repeated when they are created; the section ownership table in §1.5 defines the boundaries that prevent duplication. |
| Completeness audit of the universal taxonomy | Performed — see Annex A; every taxonomy domain is mapped to a section of this document. |
| Requirement identifier audit | Performed — 436 unique requirement identifiers; no duplicates; identifiers are stable (Annex B). |
| Current-vs-future honesty audit | Performed — no capability is claimed as implemented (§1.3, §13.2, §35). |

### D.3 Sibling documents still to be authored

| Document | Must be consistent with |
|---|---|
| `ARCHITECTURE.md` | §4.5 (one model per concern), §13.39 (engine composition), §18 (execution), §27 (authorization boundaries), OQ-003, OQ-005, OQ-011, OQ-015, OQ-017, OQ-018. |
| `RULES.md` | §6 (principles), §37 (constraints) — engineering invariants may be stricter but must not contradict this document. |
| `DESIGN.md` | §9 (personas), §12 (journeys), §30 (reporting), §31 (dashboards), §27.7 (human oversight), OQ-007, OQ-010, OQ-019, OQ-021. |
| `PHASES.md` | §35 (horizons), Annex A horizons, OQ-008, OQ-009, OQ-018. |
| `DATABASE.md` | §19 (evidence model), §20 (finding model), §23 (historical intelligence), OQ-004. |
| `API.md` | §18 (execution contracts), §30.2 (report formats), §32.2 (integration contract), OQ-006. |
| `SECURITY.md` | §26.4 (prompt injection), §27 (authorization and safety), OQ-003, OQ-010, OQ-014, OQ-016, OQ-019, OQ-020. |
| `TESTING.md` | §18.7 (verifying the verification platform), §34.4 (platform reliability metrics). |
| `DEPLOYMENT.md` | §33 (non-functional requirements), §37.4 (restricted environments), OQ-002, OQ-011, OQ-014, OQ-016. |
| `CHANGELOG.md` | Any claim of delivered capability must be verifiable; no capability may be marked delivered on the basis of this PRD alone. |

### D.4 Governing statement

This document is the authoritative product definition. Where a sibling document, implementation, or workflow conflicts with it, the conflict must be resolved explicitly — by revising this document with justification, or by correcting the conflicting artifact. Silent divergence is a defect.

Unless explicitly marked CURRENT with repository evidence, everything defined here is intent, not implementation.
