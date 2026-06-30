# TASKS — question-prompt-lists

> Status: Draft · Version: 0.1.0 · Last updated: 2026-06-28 · Owner: J. Carter (acting maintainer) · Lane: donated
> Risk tier: **HIGH** for all patient-facing sets (dual expert sign-off is BLOCKING)

The backlog for the `question-prompt-lists` good-deed project. Read alongside [PLAN.md](./PLAN.md).
Milestones (M0–M3) match the roadmap there. IDs use the slug **`qpl`**; the `project` field is the
full slug `question-prompt-lists`.

## How these tasks map to Elyos

Each task below becomes an **Elyos Task JSON** validated against `packages/schema/src/schemas.ts`.
Field mapping:

- **id** — stable slug id, e.g. `qpl-sources-001` (table column `ID`).
- **title** — the task title.
- **project** — always `question-prompt-lists`.
- **type** — one of `code | research | writing | data | design-spec | maintenance` (table `Type`).
- **lane** — `donated` for all current tasks (no funded/API execution). Funded tasks would need
  `fundedBudgetUsd`; none here.
- **priority** — `high | medium | low`.
- **domain** — array, e.g. `["cancer","patient-education","oncology","health-communication"]`.
- **riskTier** — `low | medium | high`. **Every patient-facing QPL set is `high`** (dual expert
  sign-off). Taxonomy/style-guide/rubric that *shape* patient content are `medium`; pure
  tooling/process are `low` (table `Risk`).
- **urgent** — boolean (default `false`; no live emergency).
- **deliverable** — `pr | dataset | document | translation` (table `Deliverable`). QPL sets are
  authored content → `document`; structured data files → `dataset`; tooling → `pr`.
- **tokenEstimate** — `small | medium | large` (table `Size`).
- **status** — `open | in-progress | review | delivered | done` (all start `open`).
- **context / objective** — why + what.
- **acceptanceCriteria[]** — checkable bullets (listed below tables for key tasks).
- **resources[]** — links/paths (allow-list, taxonomy, style guide, source URLs, templates).
- **output** — path/description of the produced artifact.
- **requestor** — partner/requestor; `TO BE SECURED` until confirmed.
- **verifiedNeed** — boolean; **`false`** wherever value depends on an unsecured partner.
- **outputLicense** — **CC BY 4.0** for QPL content; **MIT** for code/tooling; project-metadata
  datasets (allow-list, taxonomy) are MIT.

---

## Milestone M0 — Foundation & cold-start (no partner; reviewers required for the pilot)

Goal: stand up taxonomy/schema/style-guide/allow-list/rubric/support-directory, recruit first
reviewers, and prove the pipeline on **one** general pilot set with **dual expert sign-off**.

| ID | Title | Type | Size | Risk | Deliverable | Depends on | Reviewer |
|---|---|---|---|---|---|---|---|
| qpl-sources-001 | Build source allow-list (open/PD vs reference-only; aggregate-stat stance; snapshots) | data | small | low | dataset | — | Maintainer / License reviewer |
| qpl-taxonomy-001 | Topic × journey-stage taxonomy (controlled vocab) | data | small | medium | dataset | — | Clinician + Maintainer |
| qpl-schema-001 | QPL content schemas + minimal CI structural check | code | medium | low | pr | taxonomy-001 | Maintainer |
| qpl-style-001 | Question-writing style guide (questions-not-answers, neutral, plain-language, provenance, sensitive content) | writing | small | medium | document | — | Clinician + Advocate |
| qpl-rubric-001 | Expert-review rubric + reviewer-handoff template (dual sign-off, COI, conflict resolution) | writing | small | medium | document | style-001 | Clinician + Advocate |
| qpl-support-001 | Verified crisis/support-resource directory (≥1 region) | data | small | medium | dataset | — | Maintainer / Advocate |
| qpl-reviewers-001 | Recruit + onboard ≥1 oncology clinician + ≥1 patient advocate (COI) | research | medium | low | document | rubric-001 | Maintainer |
| qpl-set-001 | Pilot set: "Newly diagnosed — questions for your first oncology appointment" (general) | writing | medium | **high** | document | sources-001, taxonomy-001, schema-001, style-001, rubric-001, support-001, reviewers-001 | Oncology clinician + Patient advocate |
| qpl-watcher-001 | Minimal source-change re-fetch check (hash-diff) [automated in M1] | code | small | low | pr | sources-001, schema-001 | Maintainer |

**Acceptance criteria — key M0 tasks**

`qpl-sources-001` (allow-list)
- `sources/allow-list.yaml` lists ≥ 5 sources, each typed `open | public-domain | reference-only`,
  including ≥ 1 NCI/PD source and the **SEER + GLOBOCAN aggregate-stat** stance recorded.
- Each entry records: name, canonical URL, version/date, retrieval date, license name + URL,
  **snapshot of license/source text**, `snapshotHash` (SHA-256), `snapshotArchiveUrl` where
  available, `derivativesAllowed`, attribution string, `dataKind` (text|aggregate-stat),
  `verifiedBy`, `verifiedDate`.
- **Copyrighted QPL sources (ACS, ASCO/Cancer.Net, NCCN, Macmillan, CRUK, ESMO) are marked
  `reference-only`** with an explicit "do not copy/recompile" note; **AJCC** marked excluded from
  reproduction.
- Any source with unclear/incompatible terms is marked **excluded** with a reason.

`qpl-taxonomy-001` (taxonomy)
- `taxonomy/journey-stages.yaml` + `taxonomy/topics.yaml` define the controlled vocabularies from
  PLAN (newly-diagnosed … end-of-life; topic themes), using **public/generic** staging vocabulary
  (no AJCC tables).
- Validated by a clinician for clinical sensibility; validates against `taxonomySchema` in CI.

`qpl-set-001` (pilot set — HIGH risk)
- One **general** set authored as **original** questions grouped by topic, in `sets/...set.yaml`,
  validating against `qplSetSchema`.
- Contains the verbatim **"education, not medical advice — consult your care team"** disclaimer;
  contains **no answers/recommendations/prognoses**.
- Every framing claim/question rationale has **provenance** to an allow-listed source;
  **original-authorship attestation** present (no copyrighted QPL copied).
- Agent **`UNCERTAIN:` flags** captured into the set's `review.agentFlags`; **no sign-off while any
  flag is unresolved.**
- **Clinician sign-off AND patient-advocate sign-off** recorded in the `review` block + PR, each with
  COI declaration; reviewers independent of the drafting step. Verified **support resources** present.
- Readability + accessibility checks pass; `lastReviewedDate` + `nextReviewDue` set. `verifiedNeed:
  false` (no partner); adoption deferred to M2.

`qpl-reviewers-001` (recruit reviewers — BLOCKING for any set)
- ≥ 1 credentialed oncology clinician and ≥ 1 trained patient advocate onboarded, each with a
  recorded **COI declaration** and agreement to the rubric; roster recorded (contacts out-of-band).
- Defines how **topic-appropriate** coverage (palliative, genetics, paediatric) will be sourced
  before any matching set is built.

**M0 Definition of Done:** allow-list (≥5 verified sources, snapshots) + taxonomy + content schemas
+ minimal CI check + style guide + review rubric + verified support directory merged; ≥1 clinician +
≥1 advocate recruited; **one general pilot set authored and dual-signed-off** with disclaimer,
provenance, support resources, and readability/a11y passing; minimal source-change check green.
**No set was shipped without dual sign-off.** All M0 set deliverables carry `verifiedNeed: false`.

---

## Milestone M1 — Repeatability, reviewer panel & quality automation

Goal: make the pipeline repeatable and harden the gates.

| ID | Title | Type | Size | Risk | Deliverable | Depends on | Reviewer |
|---|---|---|---|---|---|---|---|
| qpl-reviewers-002 | Grow reviewer panel to ≥4 (specialty mix) + rotation | research | medium | low | document | reviewers-001 | Maintainer / Steward |
| qpl-sets-002 | Author 3–4 more general sets across ≥3 journey stages | writing | large | **high** | document | set-001 | Clinician + Advocate |
| qpl-a11y-001 | Automate readability + accessibility checks in CI | code | medium | low | pr | schema-001 | Maintainer |
| qpl-license-001 | Automate license/provenance enforcement (attestation, provenance, disclaimer, support presence) | code | medium | low | pr | schema-001, sources-001 | Maintainer / License reviewer |
| qpl-watcher-002 | Automate source-change watcher (scheduled hash-diff vs snapshots) | code | small | low | pr | watcher-001 | Maintainer |
| qpl-runbook-001 | End-to-end pipeline runbook | writing | small | low | document | set-001, license-001 | Maintainer |

**Acceptance criteria — key M1 tasks**

`qpl-license-001`
- CI fails any set missing the **disclaimer**, **provenance** on a flagged assertion, the
  **dual `review` sign-off block**, `nextReviewDue`, or (for sensitive sets) **verified support
  resources**; and fails if an **original-authorship attestation** is absent.
- Cross-checks each set's source references against allow-list entries (type + terms).

`qpl-sets-002`
- 3–4 additional **general** sets, each original, dual-signed-off, with provenance, disclaimer,
  support resources, readability/a11y passing, validating against `qplSetSchema`.
- Coverage spans ≥ 3 distinct journey stages; any sensitive set has the **topic-appropriate**
  credentialed reviewer.

`qpl-reviewers-002`
- Panel ≥ 4 (≥2 clinicians across relevant specialties + ≥2 advocates) or a reviewing partner org
  engaged; rotation + load-balancing and conflict-resolution escalation path documented.

**M1 Definition of Done:** reviewer panel ≥4 (or reviewing partner) with rotation; 3–4 more
dual-signed-off general sets across ≥3 stages; readability/a11y + license/provenance enforcement
**automated in CI**; source-change watcher automated; runbook merged. **Steward named** (prerequisite
for M2).

---

## Milestone M2 — First partner adoption (needs partner)

Goal: deliver adopted sets to real patients. **All tasks gated on a secured partner**
(`verifiedNeed` flips to `true` only when confirmed).

| ID | Title | Type | Size | Risk | Deliverable | Depends on | Reviewer |
|---|---|---|---|---|---|---|---|
| qpl-partner-001 | Secure first partner; agree population/stage/topic + distribution + feedback | research | medium | low | document | reviewers-002 | Steward / Maintainer |
| qpl-sets-003 | Author partner-priority set(s) for agreed population/stage | writing | large | **high** | document | partner-001, license-001 | Clinician + Advocate |
| qpl-delivery-001 | Package, deliver, and confirm partner adoption + patient feedback loop | writing | small | medium | document | sets-003 | Steward |

**Acceptance criteria — key M2 tasks**

`qpl-partner-001`
- A named clinic/advocacy org confirmed in writing as requestor; agreed **population, journey
  stage(s), topics**, distribution channel, and a **PII-safe** feedback method (no patient data to
  Elyos). On completion, related tasks update `requestor` + `verifiedNeed: true`.
- **Pause/decision point honored:** if no partner by end of M1, the documented **go/pivot/hold**
  decision is recorded before further set work.

`qpl-delivery-001`
- Delivered set(s) include questions, disclaimer, provenance, dual sign-off, support resources;
  license/provenance CI green; **partner confirms adoption (given to patients) in writing** (recorded
  in PR/receipt). First true **Definition of Shipped** event.

**M2 Definition of Done:** partner secured (`verifiedNeed=true`); ≥ 1 dual-signed-off,
correctly-licensed set **delivered and confirmed adopted** (given to patients); PII-safe feedback
loop established.

---

## Milestone M3 — Scale, type-specific sets, and translation

Goal: scale coverage with sustained quality.

| ID | Title | Type | Size | Risk | Deliverable | Depends on | Reviewer |
|---|---|---|---|---|---|---|---|
| qpl-sets-004 | Cancer-type-specific sets (topic-appropriate reviewers) | writing | large | **high** | document | delivery-001 | Specialty clinician + Advocate |
| qpl-refresh-001 | Review-refresh cadence + stale-set auto-flagging + withdrawal procedure | maintenance | small | low | document | set-001 | Maintainer |
| qpl-outcomes-001 | Outcome tracking: post-publication defect + partner-feedback log + coverage matrix | data | small | low | dataset | delivery-001 | Steward |
| qpl-translate-001 | Translation pilot for ≥1 set under a separate high-risk translation gate | translation | large | **high** | translation | delivery-001 | Medical-translation reviewer + Clinician |

**Acceptance criteria — key M3 tasks**

`qpl-translate-001`
- Reuses the `vital-info-translations` review model: **qualified medical-translation reviewer**, plus
  **back-translation QA** for any sensitive (prognosis/end-of-life) content, plus the original set's
  clinician endorsement of meaning preservation; disclaimer + support resources localized + verified
  for the target region.

`qpl-refresh-001`
- Documented cadence to re-review each set ≤ 12 months / on guideline change; CI/script
  **auto-flags** sets past `nextReviewDue`; defines **withdrawal / under-re-review** procedure when
  guidance or a source license changes.

**M3 Definition of Done:** ≥ 6 sets adopted across ≥ 3 stages; ≥ 1 type-specific set; refresh cadence
+ stale-flagging live; outcome tracking live; ≥ 1 translation piloted under the high-risk gate;
named sustainability owner.

---

## Backlog / future

Sized but unscheduled:

- **(medium) Caregiver-specific variants** of high-value sets (distinct audience framing).
- **(medium) Printable / large-print / screen-reader-optimized render templates** beyond plain Markdown.
- **(large, partner-driven) Setting-specific tailoring** (e.g., paediatric/AYA, community-clinic
  short-visit versions) — each needs the topic-appropriate reviewer.
- **(medium) Additional regions' support/crisis directories** as partners expand geographically.
- **(small) Coverage-matrix dashboard** (open, static) showing topic × stage completion + currency.
- **(large, funded — needs escrow)** Surge authoring under the funded lane (metered, hard
  `fundedBudgetUsd` cap) for a high-demand event — out of scope for v0.1.

---

## Example task JSON

Schema-valid Task JSON for the first M0 task. `verifiedNeed` is **false** (no partner secured);
`outputLicense` is **MIT** because the allow-list is project metadata, not patient-facing CC-BY content.

---

## Generated task index

Generated by Elyos task-decomposition agent on 2026-06-29. All files in `tasks/` are schema-valid
against `packages/schema/src/schemas.ts` (draft-07, `additionalProperties:false`). 22 total
(1 seed + 21 generated). No fan-out dimensions were explicitly enumerated in the backlog tables.

| File | Milestone | Type | Risk | Deliverable | Priority | verifiedNeed |
|---|---|---|---|---|---|---|
| tasks/qpl-sources-001.json | M0 | data | low | dataset | high | false |
| tasks/qpl-taxonomy-001.json | M0 | data | medium | dataset | high | false |
| tasks/qpl-schema-001.json | M0 | code | low | pr | high | false |
| tasks/qpl-style-001.json | M0 | writing | medium | document | high | false |
| tasks/qpl-rubric-001.json | M0 | writing | medium | document | high | false |
| tasks/qpl-support-001.json | M0 | data | medium | dataset | high | false |
| tasks/qpl-reviewers-001.json | M0 | research | low | document | high | false |
| tasks/qpl-set-001.json | M0 | writing | **high** | document | high | false |
| tasks/qpl-watcher-001.json | M0 | code | low | pr | high | false |
| tasks/qpl-reviewers-002.json | M1 | research | low | document | high | false |
| tasks/qpl-sets-002.json | M1 | writing | **high** | document | high | false |
| tasks/qpl-a11y-001.json | M1 | code | low | pr | high | false |
| tasks/qpl-license-001.json | M1 | code | low | pr | high | false |
| tasks/qpl-watcher-002.json | M1 | code | low | pr | high | false |
| tasks/qpl-runbook-001.json | M1 | writing | low | document | high | false |
| tasks/qpl-partner-001.json | M2 | research | low | document | medium | false |
| tasks/qpl-sets-003.json | M2 | writing | **high** | document | medium | false |
| tasks/qpl-delivery-001.json | M2 | writing | medium | document | medium | false |
| tasks/qpl-sets-004.json | M3 | writing | **high** | document | low | false |
| tasks/qpl-refresh-001.json | M3 | maintenance | low | document | low | false |
| tasks/qpl-outcomes-001.json | M3 | data | low | dataset | low | false |
| tasks/qpl-translate-001.json | M3 | writing | **high** | translation | low | false |

> Note: `qpl-translate-001` uses `type: "writing"` + `deliverable: "translation"` per schema
> (the schema enum does not include a "translation" type; translation tasks use writing+translation).
> All `verifiedNeed: false` — no partner or reviewer is secured as of 2026-06-28.

---

## Example task JSON

Schema-valid Task JSON for the first M0 task. `verifiedNeed` is **false** (no partner secured);
`outputLicense` is **MIT** because the allow-list is project metadata, not patient-facing CC-BY content.

```json
{
  "id": "qpl-sources-001",
  "title": "Build source allow-list (open/PD vs reference-only; aggregate-stat stance; snapshots)",
  "project": "question-prompt-lists",
  "type": "data",
  "lane": "donated",
  "priority": "high",
  "domain": ["cancer", "patient-education", "oncology", "licensing"],
  "riskTier": "low",
  "urgent": false,
  "deliverable": "dataset",
  "tokenEstimate": "small",
  "status": "open",
  "context": "question-prompt-lists authors ORIGINAL, openly-licensed 'questions to ask your oncologist' sets grounded in authoritative sources. Source material is NOT uniformly reusable: NCI/Cancer.gov/PDQ text is generally US public domain (verify trademark/embedded media), SEER and GLOBOCAN are AGGREGATE statistics (verify per-use terms; GLOBOCAN often non-commercial), while ACS/ASCO-Cancer.Net/NCCN/Macmillan/Cancer Research UK/ESMO patient QPLs are COPYRIGHTED and must be reference-only (never copied or recompiled), and AJCC staging tables are excluded from reproduction. Controlled-access or identifiable patient data is strictly out of scope. Nothing may be used until its source is allow-listed with verified terms.",
  "objective": "Create a structured, per-source allow-list that records each source's type (open | public-domain | reference-only), license terms, derivatives permission, required attribution, dataKind (text | aggregate-stat), and a hash/archived snapshot, so the per-set license and provenance gate can be checked consistently and copyrighted QPLs are never copied.",
  "acceptanceCriteria": [
    "sources/allow-list.yaml lists >= 5 sources, each typed open|public-domain|reference-only, including >= 1 NCI/public-domain source and the SEER + GLOBOCAN aggregate-stat stance recorded",
    "Each entry records: name, canonical URL, version/date, retrieval date, license name + URL, snapshot of license/source text, snapshotHash (SHA-256), snapshotArchiveUrl where available, derivativesAllowed, attribution string, dataKind, verifiedBy, verifiedDate",
    "Copyrighted QPL sources (ACS, ASCO/Cancer.Net, NCCN, Macmillan, Cancer Research UK, ESMO) are marked reference-only with an explicit do-not-copy/recompile note; AJCC marked excluded from reproduction",
    "Any source with unclear or incompatible terms is marked excluded with a reason",
    "File validates against sourceAllowListSchema and passes CI structural checks"
  ],
  "resources": [
    "C:/code/elyos/planning/projects/question-prompt-lists/PLAN.md",
    "C:/code/elyos/planning/ROADMAP.md",
    "NCI / Cancer.gov / PDQ public-domain notice (verify trademark and embedded-media exceptions)",
    "SEER citation/usage terms; GLOBOCAN / IARC usage terms (verify per use)"
  ],
  "output": "sources/allow-list.yaml plus a short README documenting the allow-list schema, the open/PD-vs-reference-only distinction, and the verification process",
  "requestor": "TO BE SECURED",
  "verifiedNeed": false,
  "outputLicense": "MIT"
}
```
