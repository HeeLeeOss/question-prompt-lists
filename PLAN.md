# PLAN — question-prompt-lists

> Status: Draft · Version: 0.1.0 · Last updated: 2026-06-28 · Owner: J. Carter (acting maintainer) · Lane: donated
> Risk tier: **HIGH** (patient-facing health content — see Quality, review & risk gates)

## Executive summary

`question-prompt-lists` is an Elyos good-deed project that produces **open, freely reusable
"questions to ask your oncologist" prompt sets**, organized by **topic** (e.g., understanding the
diagnosis, treatment options, side effects, clinical trials, genetics, cost, fertility,
survivorship, palliative/end-of-life) and by **stage of the cancer journey** (newly diagnosed,
staging, treatment decision, on-treatment, recurrence, survivorship, advanced/end-of-life). A
**question prompt list (QPL)** is an evidence-based communication aid: a structured set of
questions a patient or caregiver can bring to an appointment so they participate more fully,
remember what to ask, and have a better conversation with **their own care team**. QPLs are a
well-studied intervention in oncology communication research, where they have been associated with
greater patient question-asking and information recall. **This project produces questions, never
answers.**

The defining principle is therefore: **questions, not advice.** We do not tell anyone which
treatment to choose, what their prognosis is, or what to do. We give patients better questions to
ask the clinicians who can answer them. Every patient-facing artifact carries the standing
disclaimer **"This is education, not medical advice — always consult your own care team,"** and is
**reviewed and signed off by a credentialed oncology clinician *and* a patient advocate before it
ships** (high risk tier; blocking).

The second defining constraint is **license and provenance discipline under cancer-domain
guardrails.** Many of the best-known QPLs (American Cancer Society, ASCO/Cancer.Net, NCCN,
Macmillan, Cancer Research UK) are **copyrighted** and may **not** be copied or re-arranged into a
derivative compilation. We therefore **author original questions**, grounded in **authoritative,
verifiable sources**, and we use only **open-access / public-domain reference material** and
**aggregate, de-identified statistics** (e.g., SEER, GLOBOCAN) for context and prioritization.
**Controlled-access or identifiable patient data is strictly out of scope.** Every assertion that
appears in framing text or in a question's rationale carries **provenance**; any question we cannot
ground and an expert cannot endorse is not published.

The work runs in the **donated lane**: a human runs their own coding agent to draft QPL content and
tooling, then opens PRs; the Elyos CLI only prepares workspaces and opens PRs. It never invokes an
agent and never runs headless.

Honest status note: **no partner clinic or advocacy organization, and no expert reviewer, is yet
secured.** Because the deliverable is high-risk patient-facing health content, **nothing reaches
"shipped" without credentialed expert sign-off and real-world adoption.** Until reviewers and a
partner exist, `verifiedNeed` is recorded as `false` on tasks whose value depends on a named
beneficiary, and the foundation milestones (taxonomy, schema, style guide, source allow-list,
review rubric, verified helpline directory) are built so the project makes honest progress
*without* shipping unreviewed advice. No originating proposal exists in
`governance/proposals/` yet (the project appears only in the portfolio roadmap); writing that
proposal is an open dependency.

## Problem & beneficiaries

**Who is helped.** Cancer patients and their caregivers preparing for oncology appointments —
especially people who are newly diagnosed, overwhelmed, time-pressured in short consultations, have
**limited health literacy**, face a **language barrier**, or are navigating a **rare cancer** or a
**high-stakes decision point** (treatment choice, recurrence, transition to palliative care). The
ultimate beneficiaries are **patients in the consulting room** who today often leave without asking
what mattered most, forget two-thirds of what was said, or do not know that a question (a clinical
trial, a second opinion, fertility preservation before treatment, the cost of care) was even theirs
to ask.

**The need.** Decades of communication research describe the same gap: patients under stress
ask few questions, recall little, and defer to clinicians even when a decision is genuinely theirs
to share. **Question prompt lists are an evidence-based, low-cost intervention** designed to close
exactly this gap, and they are recommended in patient-centred-care guidance. But the freely
**reusable, openly-licensed, structured, and translatable** supply is thin: the most visible QPLs
are copyrighted, English-only, locked in PDFs, not machine-readable, and not maintained as open
data that clinics or translators can adapt. The gap this project fills is **open, sourced,
expert-reviewed, structured QPL content** that anyone — a clinic, an advocacy group, a translator —
can adopt and adapt without legal risk.

**Verified need: TO BE SECURED.** The *category* need is strongly evidenced by the research
literature. But a **specific requesting clinic/advocacy organization, a confirmed patient
population, and a prioritized topic/stage list are not yet secured.** We treat that honestly:
foundation tasks proceed without a partner; **adoption and delivery tasks are blocked** until a
partner is confirmed, and they carry `verifiedNeed: false` until then.

**Partner org: TO BE SECURED.** Candidate partner types: hospital cancer-centre patient-education
departments, disease-specific foundations (e.g., a sarcoma or lung-cancer foundation), national
cancer charities, patient-navigator programs, and community oncology clinics. **Expert-reviewer
partners** (volunteer medical/clinical/radiation oncologists, oncology nurses, genetic counsellors,
and trained patient advocates) are a parallel, equally-blocking dependency. None is committed as of
this draft.

## Goals and non-goals

**Goals**
- Produce **original, openly-licensed (CC BY 4.0) QPL sets** organized by topic and by journey
  stage, as **structured, machine-readable data** that renders to plain-language, printable, and
  screen-reader-friendly formats.
- Ground every set in **authoritative, verifiable sources**, with **provenance on every assertion**
  and a clear "questions, not answers" framing.
- Gate every patient-facing set behind **credentialed oncology-clinician sign-off *and* patient-advocate
  sign-off** (high risk tier) before it ships.
- Embed the standing **"education, not medical advice — consult your care team"** disclaimer and,
  where a set touches distress/prognosis/end-of-life, **verified crisis and support-line resources**.
- Meet a **plain-language / health-literacy** bar (target reading level and accessibility) so the
  questions are usable by the people who need them most.
- Deliver sets that a partner clinic/advocacy org **actually adopts and gives to patients**, and
  make the content **translation-ready** for later localization.

**Non-goals**
- **Not medical advice.** We never recommend a treatment, estimate a prognosis, interpret a
  patient's results, or answer the questions we pose. (Doing so would be unqualified high-stakes
  advice and is refused.)
- **Not** copying or re-compiling copyrighted QPLs (ACS, ASCO/Cancer.Net, NCCN, Macmillan, CRUK,
  ESMO, etc.). We author original questions; copyrighted material is **reference-only**.
- **Not** using controlled-access or **identifiable patient data** of any kind (dbGaP/EGA/biobanks,
  individual records). Only **open-access / aggregate / de-identified** sources (SEER, GLOBOCAN).
- **Not** a diagnostic, triage, symptom-checker, or chatbot; **not** a substitute for a clinician.
- **Not** a directory of providers, drugs, brands, or products; **no** steering toward any
  for-profit treatment, trial sponsor, or service.
- **Not** authoring clinical-decision content, guideline summaries, or "what the answer should be"
  explainers (those are different, higher-bar projects).
- **Not** a hosted website, app, or patient-data store in v0.1 (delivery is open content + adoption
  by partners).
- **Not** providing legal, immigration, or financial advice (cost questions are framed as questions
  to ask, e.g., a financial navigator — never as advice).

## Success metrics (outcomes)

Outcome-based and beneficiary-centric. Baselines are ~0 (new project). **Outcome** targets are for
the first ~6 months after reviewers **and** a partner are secured; **interim foundation metrics**
are tracked from M0/M1 so progress is visible *before* a partner exists. We explicitly **do not**
count "PRs merged," "questions written," or "sets drafted" as success — only **expert-reviewed,
correctly-licensed sets adopted and given to patients.**

**Outcome metrics (post-reviewer + post-partner)**

| Metric | Baseline | Target | How measured |
|---|---|---|---|
| QPL sets with **dual expert sign-off** (oncology clinician + patient advocate) | 0 | ≥ 6 sets | `review` block in each set + signed PR |
| QPL sets **adopted by a partner** and given to patients | 0 | ≥ 3 sets in ≥ 1 setting | Partner written confirmation in PR/receipt |
| Topic × journey-stage **coverage** (cells filled, expert-reviewed) | 0 | ≥ 6 cells across ≥ 3 stages | Coverage matrix in repo |
| **Critical content defects** found *after* publication (embedded advice, factual error, leading/biased question, missing disclaimer) | n/a | **0** (hard gate) | Post-publication defect log |
| Patient/caregiver-reported **usefulness** ("helped me ask what mattered") | n/a | Positive from a partner sample | Partner-run feedback (no PII to Elyos) |
| Sets within their **review-refresh window** (re-reviewed ≤ 12 months / on guideline change) | n/a | 100% | `nextReviewDue` audit |
| **Plain-language target met** (reading level + accessibility checks) | n/a | 100% of published sets | Readability + a11y check in CI + advocate sign-off |

**Interim foundation metrics (M0/M1, partner-independent)**

| Metric | Baseline | Target | How measured |
|---|---|---|---|
| Authoritative sources **verified** and recorded on the allow-list | 0 | ≥ 5 by end of M0 | Allow-list entries w/ `verifiedBy`/`verifiedDate` |
| Expert reviewers **recruited & onboarded** (≥1 oncology clinician + ≥1 advocate) | 0 | ≥ 2 by end of M0; panel ≥ 4 by M1 | Reviewer roster + COI declarations |
| Crisis/support resources **verified current** | 0 | ≥ 1 verified directory by end of M0 | Helpline directory w/ verified dates |
| First pilot set passing **dual sign-off** | 0 | 1 by end of M0 | Signed PR |

**Sample rule.** Outcome percentages are reported only once the relevant denominator is ≥ 5
published sets; below that we report raw counts (e.g., "3/4 within window") to avoid small-sample
noise. The "0 critical defects" gate is reported from the first published set.

## Scope

**Definition — "journey stage" (the row axis).** A controlled vocabulary, expert-validated in M0:
`newly-diagnosed`, `staging-workup`, `treatment-decision`, `on-treatment`, `managing-side-effects`,
`clinical-trials`, `genetics-hereditary`, `second-opinion`, `cost-financial`,
`fertility-preservation`, `survivorship`, `recurrence`, `palliative-supportive`, `end-of-life`.
Stage names use **plain, generic** terms; clinical staging itself uses **public** vocabulary (e.g.,
SEER Summary Stage / generic "early / locally advanced / metastatic") — **not** the copyrighted
**AJCC** staging tables.

**Definition — "topic" (the column axis).** Cross-cutting themes a question belongs to (diagnosis
understanding, treatment options, risks/benefits, side effects, prognosis discussion, supportive
care, logistics/cost, family/genetics, etc.). A set is a curated selection along topic × stage,
optionally scoped to `general` or to a **specific cancer type**.

**Prioritization rule.** Build order: (1) a **secured partner's** stated population/stage; (2)
**high-impact, high-uncertainty decision points** that the literature shows patients most struggle
to navigate (newly-diagnosed, treatment-decision, clinical-trials); (3) **general-purpose** sets
reusable across cancer types before type-specific ones; (4) sets whose **expert reviewer coverage**
is already available. Type-specific and **translated** sets come later (translation is a separate
high-risk gate, see Roadmap M3).

**In scope**
- **Original** QPL sets (questions + neutral framing intro + disclaimer + provenance + verified
  support resources + expert sign-off), authored from authoritative sources.
- A **topic × journey-stage taxonomy** and a **machine-readable QPL content schema**.
- A **question-writing style guide** (neutral/non-leading, plain-language, "questions-not-answers",
  disclaimer + provenance rules, sensitive-content handling).
- A **source allow-list** distinguishing **open/public-domain reusable** sources from
  **reference-only** copyrighted ones, with verified terms.
- A **verified crisis/support-resource directory** (helplines, support lines) with verified dates.
- An **expert-review rubric** and sign-off workflow; **structural CI validation** of QPL files;
  **readability/accessibility** checks.

**Out of scope**
- Any **answer, recommendation, prognosis, or interpretation** of a patient's situation.
- **Copying/adapting** copyrighted QPLs or building a derivative compilation of them.
- **Controlled-access or identifiable patient data**; any individual-level record.
- Reproducing **AJCC** staging tables or other copyrighted clinical instruments.
- Provider/drug/brand directories; sponsor or product steering.
- Hosting, an app, telemetry, or collecting any patient data.
- Translation/localization in v0.1 (sets are *built* translation-ready; actual translation is a
  later high-risk milestone, coordinated with `vital-info-translations`-style review).
- Topics requiring sign-off the project cannot obtain (e.g., paediatric-specific clinical nuance
  without a paediatric-oncology reviewer) — not shipped until that reviewer exists.

## Solution approach & architecture

This is primarily a **content/data project** (deliverables are structured QPL content + supporting
data), with light tooling for validation. It rides on existing Elyos donated-lane mechanics (CLI
prepares workspace, human runs their agent, PR opened, human + **expert** review gate "done").

**Pipeline (per QPL set)**
1. **Select cell & sources** — choose a topic × journey-stage (× optional cancer type) per the
   prioritization rule; confirm sources are on the allow-list (open/PD reusable vs reference-only);
   record provenance (URL, version/date, retrieval date, license snapshot).
2. **Author questions (original)** — draft questions per the **style guide**: neutral, non-leading,
   plain-language, *questions not answers*; group by topic; attach provenance to any framing claim
   or question rationale; **emit explicit `UNCERTAIN:` flags** for anything not confidently grounded.
3. **Self-check** — run the review rubric as a first pass; run **readability + accessibility**
   checks; confirm disclaimer present and **verified support resources** attached where the set
   touches distress/prognosis/end-of-life.
4. **Dual expert review (blocking)** — a **credentialed oncology clinician** verifies clinical
   accuracy, appropriateness, and absence of embedded advice/leading framing; a **patient advocate**
   verifies plain-language, tone, sensitivity, and patient-centredness. Both record sign-off + COI
   in the set's `review` block and in the PR. Unresolved `UNCERTAIN:` flags **block** sign-off.
5. **License & provenance check** — confirm output license, original-authorship attestation
   (no copyrighted QPL copied), provenance complete, disclaimer + verified support resources present.
6. **Package & deliver** — render printable/plain/screen-reader formats; hand off to partner;
   record adoption and set `nextReviewDue`.

**Artifacts / data model** (all UTF-8; YAML/JSON canonical, Markdown rendered)
- `sources/allow-list.yaml` — `{ id, name, url, type: open|public-domain|reference-only,
  licenseName, licenseUrl, reuseTerms, derivativesAllowed, attributionTemplate, snapshotHash,
  snapshotArchiveUrl, dataKind: text|aggregate-stat, verifiedBy, verifiedDate, notes }`.
- `taxonomy/journey-stages.yaml`, `taxonomy/topics.yaml` — controlled vocabularies (expert-validated).
- `sets/<stage>/<topic-or-cancer>/set.yaml` — a QPL set: `{ id, title, journeyStage, topics[],
  appliesTo: ["general"|<cancerType>...], audience: patient|caregiver, introFraming, disclaimer,
  questions[], supportResources[], provenance[], review{...}, readingLevel, lastReviewedDate,
  nextReviewDue, status, outputLicense }`.
- A **question** = `{ id, text, topic, appliesToStages[], appliesToTypes[], rationale?,
  provenanceRefs[], sensitivity?: prognosis|end-of-life|fertility|genetics|cost }`.
- `support/resources.yaml` — verified crisis/support lines `{ name, region, contact, hours, url,
  verifiedBy, verifiedDate }`.
- `templates/review-rubric.md`, `templates/style-guide.md`, `templates/reviewer-handoff.md`.

**Content schemas & CI validation.** The Task JSON schema lives in
`packages/schema/src/schemas.ts` (AJV / JSON Schema **draft-07**). This project adds **content
schemas in the same place** — `qplSetSchema`, `qplQuestionSchema`, `sourceAllowListSchema`,
`taxonomySchema`, `supportResourceSchema`, `reviewSchema` — compiled and exposed via `validate.ts`
exactly like `taskSchema`/`registrySchema` (AJV with `ajv-formats`). A structural-check script
(wired into `pnpm test`) parses every YAML artifact to JSON and **fails CI** if a published set is
**missing the disclaimer, missing provenance on a flagged assertion, missing the `review` sign-off
block, missing a `nextReviewDue`, or (when a sensitive topic is present) missing verified support
resources.** This keeps validation **agent-neutral** and in the core schema package, not in adapters.

**Key decisions**
- **Questions, not answers** — enforced in the schema (no "answer"/"recommendation" field) and the
  style guide, and checked by experts. This is the project's safety spine.
- **Original authorship, provenance-grounded** — copyrighted QPLs are reference-only; we never copy
  or re-compile them. Each set carries an **original-authorship attestation**.
- **License/provenance as structured data** — checkable by tooling, not prose buried in docs.
- **Dual sign-off, blocking** — clinician *and* advocate; high risk tier; no exceptions for
  patient-facing sets.
- **Translation-ready, not translated** — content is structured so localization is a later,
  separately-gated step (high risk).

## Data, licensing & compliance

**This is the project's most important section, and it leads with the binding cancer-domain
guardrails. When terms or accuracy are unclear, we do not publish.**

**Binding cancer guardrails (non-negotiable):**
1. **Open-access / aggregate / de-identified data only.** Contextual statistics come from
   **aggregate** sources — **SEER** (US, NCI, public domain; citation requested) and **GLOBOCAN /
   IARC** (verify per-use terms; generally permits use with attribution, often non-commercial).
   **Controlled-access (dbGaP, EGA, individual biobanks) and any identifiable patient data are OUT
   OF SCOPE** — they need authorized access + IRB this project does not have and does not seek.
2. **No medical advice.** Patient-facing content is **education only**, framed as *questions*, and
   carries the verbatim disclaimer **"This is education, not medical advice — always consult your
   own care team."** Risk tier is **high**; **credentialed oncology-clinician + patient-advocate
   sign-off is required before merge.**
3. **Verify each source's license** before use; **provenance on every assertion**.
4. **Crisis/helpline info must be verified** (named source + verified date) and kept current.

**Sources & licenses (per-source allow-list).** Only allow-listed sources may be used, each with
**verified, recorded** terms, classified by `type`:

- **Public-domain / open (reusable):** **US National Cancer Institute (NCI) / Cancer.gov / PDQ®**
  text is generally **US public domain** and explicitly reusable (note: *PDQ* is a trademark; some
  embedded images/third-party material are not PD — verify per page). **SEER** aggregate statistics
  (public domain, citation requested). These may be **quoted/adapted with attribution** and used to
  ground topics and framing.
- **Aggregate statistics (context only):** **GLOBOCAN / IARC** — verify exact terms per use
  (attribution; often non-commercial). Used only for **aggregate** prioritization/context, never
  individual inference.
- **Reference-only (copyrighted — NOT copied):** **American Cancer Society, ASCO/Cancer.Net, NCCN
  (incl. NCCN Guidelines for Patients), Macmillan Cancer Support, Cancer Research UK, ESMO patient
  guides**, hospital QPL PDFs, and the academic QPL literature. These inform **which topics matter
  and what is clinically accurate**, but **their wording, selection, and arrangement are
  copyrighted**; we **author original questions** and never reproduce or re-compile their lists.
  A **compilation/selection** can itself be protected, so we ground in **facts and guidelines**
  (not protectable) and create an **independent arrangement**.
- **Copyrighted clinical instruments (excluded from reproduction):** **AJCC** staging tables and
  similar — we use **public/generic** staging vocabulary instead.

For **each** source we record: canonical URL, version/date, retrieval date, license name + URL, a
**snapshot of the license/source text** with a **SHA-256 `snapshotHash`** and (where possible) a
**web-archive `snapshotArchiveUrl`**, whether derivatives are permitted, the required attribution
string, `dataKind` (text vs aggregate-stat), and `verifiedBy`/`verifiedDate`. A **source-change
check** (minimal/manual in M0, automated in M1) re-fetches sources, recomputes the hash, and
**flags drift** for re-verification — important because clinical guidance changes.

**Provenance model.** Every set ships `provenance[]` linking each **framing claim or question
rationale** to a verified source entry + version. A question that asserts or implies a medical fact
(e.g., that a class of treatment exists for a situation) must cite an authoritative source **and**
be endorsed by the clinician reviewer, or it is reworded into a pure question or dropped.
**Provenance is non-optional and part of the license/quality gate.**

**Output licensing.** **Original QPL content is released CC BY 4.0**; **project tooling/code is
MIT**. Because content is **original** (not derived from copyrighted QPLs) and only grounds in
public-domain/aggregate sources, CC BY 4.0 is clean. **Where NCI/SEER text is adapted, attribution
is included; copyrighted reference sources are cited as references, never relicensed.** Each set
carries an **original-authorship attestation** (no copyrighted QPL was copied).

**Privacy / PII.** **No patient data is ingested or stored — none.** Sources are public guidance
and **aggregate** statistics only. The project collects **no end-reader data** and runs **no
telemetry**. Any partner-run patient feedback stays with the partner; only **aggregate,
de-identified** summaries (if any) ever reach Elyos. Partner/reviewer contact details are handled
out-of-band and never committed.

**Attribution & disclaimer.** Every patient-facing artifact includes: the verbatim **not-medical-advice
disclaimer**, source **attribution** for any adapted PD/open content, the **last-reviewed date** and
**next-review-due date**, and, where the set touches distress/prognosis/end-of-life, **verified
support-line resources**.

## Quality, review & risk gates

**This section leads with the cancer guardrails: patient-facing health content is HIGH risk and
expert sign-off is BLOCKING.**

**Risk tier: HIGH.** The portfolio roadmap tags this project "medium," but per the binding cancer
guardrails **all patient-facing QPL sets are treated as high risk** and **require credentialed
oncology-clinician *and* patient-advocate sign-off before merge.** (Pure tooling/taxonomy/process
tasks with no patient-facing content are low/medium and reviewed accordingly, but **no set is
published without dual expert sign-off**.) This elevation is intentional and is recorded here as the
project's standing decision.

**Required review before a set is "done"**
1. **Agent/author self-check** against the review rubric and style guide, including the
   **uncertainty self-check** (below); **readability + accessibility** checks pass.
2. **Clinician sign-off (blocking)** — a **credentialed oncology clinician** (medical/clinical/
   radiation oncologist, or oncology-credentialed clinician appropriate to the topic, e.g., a
   genetic counsellor for hereditary sets) confirms: clinical accuracy, appropriateness for the
   stage, **no embedded advice/prognosis**, no leading/biased framing, no missing critical question
   that would mislead by omission.
3. **Patient-advocate sign-off (blocking)** — a trained advocate confirms: plain language, tone,
   emotional sensitivity, cultural appropriateness, patient-centredness, and that support resources
   are present where needed.
4. **License & provenance check** — original-authorship attestation; provenance complete;
   disclaimer + verified support resources present; output license correct.
5. **CI green** — structural validation (disclaimer/provenance/review/`nextReviewDue`/support
   resources present), readability, accessibility, and any code tests pass.
6. **Maintainer approval** of the PR.

**Reviewer independence & two-discipline rule.** The clinician and advocate sign-offs are **two
distinct disciplines** and both are mandatory for any patient-facing set — **single-reviewer
sign-off is never sufficient.** Reviewers must be **independent of the drafting step** (the human
who ran the drafting agent may not be a sole sign-off reviewer) and each records a
**conflict-of-interest declaration**. **Sensitive sets** (prognosis, end-of-life, fertility,
paediatric, hereditary risk) require the **topic-appropriate credentialed reviewer** (e.g.,
palliative-care input for end-of-life; genetic counsellor for hereditary) — if unavailable, the set
is **not published**.

**Reviewer disagreement / conflict resolution.** If clinician and advocate disagree, the set
**cannot ship** until resolved: (1) reconcile against sources and the style guide, recording the
rationale; (2) escalate unresolved clinical-safety disagreements to a **second clinician or the
maintainer**; (3) **when in doubt, the more conservative reading wins** and the disputed question is
reworded or held back. Recorded in the set's `review` block.

**Agent uncertainty self-check (operationalized).** The drafting agent must emit explicit flags —
`UNCERTAIN: <location> | <type: claim|leading|advice-risk|sensitivity|source|ambiguous> | <note>` —
for anything it is unsure is grounded, neutral, or advice-free. These are copied into the set's
`review` block as `agentFlags`. **No sign-off may be recorded while any flag is unresolved**; each
must be `resolved` (with the reviewer's adjudication) or `accepted-as-is` with reasoning. Unresolved
flags **block** "done".

**Refusal triggers (project-specific).** Refuse and flag any task that would: produce an answer,
recommendation, or prognosis; copy a copyrighted QPL; steer toward a specific drug/brand/sponsor or
a for-profit; use identifiable/controlled patient data; or embed an unsourced medical claim. When in
doubt, **stop and surface the concern.**

**Definition of Shipped (project-specific).** A QPL set is *shipped* only when: acceptance criteria
met **and** **clinician + advocate sign-off recorded** **and** license/provenance/disclaimer +
verified support resources verified **and** readability/accessibility met **and** CI green **and**
the set is **adopted by a partner clinic/advocacy org and given to patients** (or published openly
with a partner committed to distribute). Merged-but-not-adopted is **not** shipped; reviewed-but-not-adopted
is "delivered," not "done".

## Roadmap & milestones

**M0 — Foundation & cold-start (no partner required; reviewers required for the pilot).**
Goal: stand up the taxonomy, schema, style guide, source allow-list, review rubric, and verified
support directory, recruit the first expert reviewers, and prove the pipeline on **one** general
pilot set end-to-end **with dual expert sign-off** (adoption deferred to M2).
Exit criteria: topic × journey-stage **taxonomy** merged (expert-validated); **QPL content schema**
+ minimal CI structural check (disclaimer/provenance/review/`nextReviewDue`/support present);
**style guide** (questions-not-answers, neutral/non-leading, plain-language, provenance, sensitive
content) merged; **source allow-list** with ≥ 5 verified sources (open/PD vs reference-only,
hash/archived snapshots, ≥1 NCI/PD and the SEER/GLOBOCAN aggregate-stat stance recorded); **verified
support-resource directory** (≥1 region, verified dates); **review rubric + reviewer-handoff**
merged; **≥ 1 oncology clinician + ≥ 1 patient advocate recruited** with COI declarations; **one
general pilot set** (e.g., "Newly diagnosed: questions for your first oncology appointment")
authored and **dual-signed-off**, with disclaimer, provenance, and support resources. `verifiedNeed`
honestly `false` (no partner). **No set ships without dual sign-off, from the very first one.**

**M1 — Repeatability, reviewer panel & quality automation.**
Goal: make the pipeline repeatable and harden quality gates.
Exit criteria: **reviewer panel ≥ 4** (≥2 clinicians across relevant specialties + ≥2 advocates) or
a reviewing partner org engaged, with rotation defined; **3–4 more general sets** across ≥ 3 journey
stages, each dual-signed-off; **readability + accessibility checks automated in CI**; **license/
provenance enforcement automated** (original-authorship attestation + provenance completeness +
disclaimer/support presence cross-checked); **automated source-change watcher** (hash-diff) running;
**pipeline runbook** merged. Dependency: reviewer recruitment.

**M2 — First partner adoption (needs partner).**
Goal: deliver adopted sets to real patients. **All tasks gated on a secured partner**
(`verifiedNeed` flips to `true` only when confirmed).
Exit criteria: a partner clinic/advocacy org secured; agreed population/stage/topic list; **≥ 1
expert-reviewed, correctly-licensed set delivered and confirmed adopted** (given to patients);
partner-run feedback loop established (no PII to Elyos). First true **Definition of Shipped** event.

**M3 — Scale, type-specific sets, and translation.**
Goal: scale coverage with sustained quality.
Exit criteria: ≥ 6 sets adopted across ≥ 3 stages; **cancer-type-specific** sets begun (each with a
topic-appropriate reviewer); **review-refresh cadence** operating (≤12 months / on guideline
change); **outcome tracking** (defect log + partner feedback) live; **translation pilot** for ≥ 1
set under a **separate high-risk translation gate** (coordinated with the `vital-info-translations`
review model: qualified medical-translation reviewer + back-translation for sensitive content);
**named sustainability owner**.

## Work breakdown

The itemized, sized backlog lives in **[TASKS.md](./TASKS.md)**, organized by the milestones above
(M0–M3) plus a Backlog/future section. Each task maps to an Elyos Task JSON (see the schema in
`packages/schema/src/schemas.ts`) with id, type, lane, risk tier, deliverable, acceptance criteria,
and license fields. M0 tasks are foundation work plus the first expert-reviewed pilot set; M2+ tasks
are gated on a secured partner and marked accordingly (`verifiedNeed: false` until then). Every
patient-facing set task carries **riskTier `high`** and a **dual-expert reviewer** requirement.

## Governance, roles & stakeholders

- **Maintainer (Owner): J. Carter (acting)** — assigned now; accepts/sequences tasks, approves PRs,
  owns the allow-list and the license/provenance gate, and **owns enforcement of the dual-sign-off
  rule** (no patient-facing set merges without it). Acts as interim license/compliance reviewer.
- **Credentialed oncology-clinician reviewer(s): TO BE SECURED** — medical/clinical/radiation
  oncologists, oncology nurses, genetic counsellors (topic-appropriate); **blocking** sign-off on
  every patient-facing set. Panel + rotation defined in M1.
- **Patient-advocate reviewer(s): TO BE SECURED** — trained advocates / patient-navigators;
  **blocking** sign-off for plain-language, tone, sensitivity, patient-centredness.
- **License/compliance reviewer** — maintainer initially; verifies source terms, original-authorship
  attestation, provenance, disclaimer + support resources.
- **Steward (last-mile owner): TBD — named by end of M1** (acting maintainer holds these duties
  meanwhile). Owns the partner relationship and confirms **adoption** (without this, nothing reaches
  "shipped"). Naming a steward is a **prerequisite for entering M2**.
- **Partner / requestor: TO BE SECURED** — clinic/advocacy org defining population/stage/topic
  priorities and confirming adoption + patient feedback.
- **Expert-reviewer recruitment** is itself a **blocking dependency**, on par with securing a
  partner — the project cannot ship *any* set without credentialed reviewers.

## Dependencies & integrations

- **Elyos donated lane**: `packages/cli` (workspace prep + PR), `packages/core`, `packages/schema`
  (Task JSON + new content schemas). No funded-lane / API-key execution in this project.
- **Public sources (read-only)**: NCI/Cancer.gov/PDQ, SEER (aggregate), GLOBOCAN/IARC (aggregate);
  copyrighted references (ACS, ASCO/Cancer.Net, NCCN, Macmillan, CRUK, ESMO) **as reference only**.
- **Expert reviewers** (oncology clinicians + patient advocates) — **external dependency, not yet
  secured; blocking for any patient-facing set.**
- **Partner clinic/advocacy org** — for requirements, adoption, and patient feedback — **not yet
  secured.**
- **Verified crisis/support directories** (e.g., national cancer support lines, 988-type crisis
  lines per region) — verified per use, kept current.
- **Plain-language / accessibility tooling** (readability scoring, accessibility linting).
- **`vital-info-translations`** — reused review model for the M3 translation pilot.

## Risks & mitigations

| Risk | Likelihood | Impact | Mitigation | Owner |
|---|---|---|---|---|
| A "question" embeds medical advice, a prognosis, or a factual error → patient harm | Medium | Critical | Questions-not-answers enforced in schema + style guide; provenance on every assertion; **blocking clinician sign-off**; `advice-risk` uncertainty flags block sign-off; 0-defect gate | Clinician reviewer / Maintainer |
| Leading/biased questions steer toward a treatment, product, or sponsor (for-profit benefit) | Medium | High | Neutrality rubric; **no brands/drugs/sponsors**; advocate review; refusal guardrail; original-authorship | Advocate / Maintainer |
| Copyright infringement by copying/re-compiling copyrighted QPLs | Medium | High | Reference-only allow-list; **original authorship + attestation**; ground in facts/guidelines, independent arrangement; license gate | License reviewer / Maintainer |
| Out-of-scope data: someone uses controlled-access/identifiable patient data | Low | Critical | Hard scope rule (aggregate/open only); allow-list `dataKind`; review checks; refusal guardrail | Maintainer |
| Outdated guidance (clinical practice changes) | High | High | `lastReviewedDate`/`nextReviewDue`; ≤12-month re-review; source-change watcher; "original is not a substitute for your team" framing | Maintainer / Reviewers |
| Harm from prognosis/end-of-life/distressing content | Medium | High | Sensitive-content handling in style guide; **verified support/crisis resources required**; topic-appropriate (e.g., palliative) reviewer; content framing | Advocate / Clinician |
| No credentialed reviewer available for a topic | High | High | Don't ship unreviewed; recruit a panel; partner with an advocacy org; scope only topics with reviewer coverage | Maintainer / Steward |
| No partner secured → nothing reaches "shipped" | High | High | M0/M1 build partner-independent value; concrete outreach plan + pause/decision point at end of M1; `verifiedNeed=false` until secured | Acting maintainer → Steward |
| Misuse: readers treat QPLs as a substitute for care | Medium | Medium | Verbatim disclaimer on every artifact; framing as a conversation aid; support resources | Maintainer |
| Accessibility/health-literacy failure (too complex to use) | Medium | Medium | Plain-language target + readability/a11y checks in CI; advocate sign-off | Advocate / Maintainer |
| Agent overconfidence / unflagged uncertainty | Medium | High | Operationalized `UNCERTAIN:` flags → `review` block; unresolved flags **block** sign-off; output treated as draft only | Reviewers |
| Crisis/helpline info wrong or stale | Medium | High | Verified directory with `verifiedDate`; re-verify on the refresh cadence; CI requires support resources on sensitive sets | Maintainer |

## Security & privacy

- **Threat surface** is small: public/aggregate source ingestion + text artifacts in a public repo.
  Primary risks are **content integrity** (embedded advice, factual/leading error, copyright) and
  **currency**, not data exfiltration.
- **No patient data, ever.** No identifiable or controlled-access data is ingested or stored; only
  open guidance + aggregate statistics. No end-reader data; **no telemetry**.
- **No secrets** in the normal flow (donated lane; no API keys/escrow). Per CLAUDE.md, never write
  secrets/tokens into logs, receipts, or committed files.
- **PII**: none ingested; partner/reviewer contacts kept out-of-band and uncommitted; any partner
  patient feedback stays with the partner (only aggregate, de-identified summaries reach Elyos).
- **Abuse/misuse prevention**: refusal guardrails apply (no advice/prognosis, no copyrighted-QPL
  copying, no for-profit steering, no controlled/identifiable data, no unsourced claims). Source
  integrity (authoritative, current, correctly-licensed) is verified per set.
- **Supply-chain**: pin source URLs + version/date; **hash/archive** license + source snapshots;
  source-change watcher (M0 minimal, M1 automated) flags drift for re-verification.

## Sustainability & maintenance

- **After delivery**, the maintainer + steward keep the allow-list, taxonomy, support directory, and
  sets current, and **re-review each set on the cadence** (≤12 months or when guidance/guidelines
  change). Reviewer **rotation** (M1/M3) avoids single-person dependence; sensitive topics keep
  topic-appropriate reviewer coverage.
- **Outcome tracking** continues post-delivery: a post-publication **defect/feedback log** per set,
  partner check-ins on continued use and usefulness, and a coverage matrix. Outcomes (adoption,
  defects, usefulness, currency) — not merge counts — are the maintained metrics.
- **Decommissioning**: if guidance changes materially or a source's license changes, affected sets
  are flagged and, if needed, **withdrawn or marked "under re-review"**; provenance makes impact
  assessment possible. Stale sets past `nextReviewDue` are automatically flagged.

## Open questions

1. **Reviewers (blocking).** Who are the first credentialed oncology clinician(s) and patient
   advocate(s)? Recruit individuals or partner with an advocacy/clinical org? What are the formal
   qualification + COI criteria, and how is topic-appropriate coverage (palliative, genetics,
   paediatric) guaranteed? **No patient-facing set ships until this is answered.**
2. **Partner (blocking for M2).** Which clinic/advocacy org is the first requestor, for what
   population/stage/topics, and how will they distribute and gather feedback?
   **Partner/reviewer-sourcing plan (concrete):**
   - **Outreach target types:** hospital cancer-centre patient-education depts, disease-specific
     foundations, national cancer charities, patient-navigator programs, community oncology clinics;
     for reviewers, professional societies' volunteer networks and advocacy-org reviewer pools.
   - **Owner:** acting maintainer until a Steward is named (end of M1), who then takes it over.
   - **Timeline:** outreach begins in parallel with M0; aim for **≥ 1 clinician + ≥ 1 advocate by
     end of M0** and **≥ 3 serious partner conversations by end of M1**.
   - **Pause/decision point:** if **no reviewers** are secured, **no patient-facing set is built**
     (foundations only). If **no partner** is secured by end of M1, the maintainer makes an explicit
     **go / pivot / hold** decision (e.g., publish openly with a distribution-committed partner, or
     hold) rather than producing sets no one will give to patients.
3. **Proposal.** No `governance/proposals/question-prompt-lists.md` exists yet — write it and
   ratify scope/risk-tier (the high-risk elevation) through governance.
4. **Risk-tier reconciliation.** Confirm with the board that this project is governed at **high**
   risk for patient-facing sets (overriding the roadmap's "medium" tag).
5. **Reading-level + accessibility targets.** Pin the exact plain-language target (e.g., grade 6–8
   equivalent) and accessibility standard, accounting for non-English readiness.
6. **Region scope for support/crisis resources.** Which region(s) first (drives helpline
   verification and partner choice)?
7. **Translation gating (M3).** Confirm the separate high-risk translation review model and which
   languages, coordinated with `vital-info-translations`.

## References

- `C:\code\elyos\CLAUDE.md` — Elyos work rules, lanes, quality bar, refusal guardrails.
- `C:\code\elyos\docs\good-deed-definition.md` — good-deed criteria and risk tiers.
- `C:\code\elyos\packages\schema\src\schemas.ts` — Task JSON schema (+ new content schemas).
- `C:\code\elyos\planning\ROADMAP.md` — portfolio + Track 8 cancer guardrails.
- `C:\code\elyos\planning\projects\vital-info-translations\PLAN.md` — reused review/license model.
- National Cancer Institute (NCI) / Cancer.gov / PDQ® — public-domain patient information (verify
  trademark/embedded-media exceptions per page).
- SEER (Surveillance, Epidemiology, and End Results) — aggregate statistics (public domain,
  citation requested).
- GLOBOCAN / IARC — aggregate global cancer statistics (verify per-use terms; often non-commercial).
- ACS, ASCO/Cancer.Net, NCCN, Macmillan, Cancer Research UK, ESMO patient guides — **reference-only**
  (copyrighted; not copied), used to verify topic relevance and clinical accuracy.
- Question-prompt-list communication research (oncology) — evidence base for the intervention.
- `governance/proposals/question-prompt-lists.md` — **to be written** (does not yet exist).

---

## Appendix A — Improvements applied

The following 25 specific improvements were identified during planning and have each been **applied
in the body above** (not left as suggestions):

1. **Risk-tier elevated to HIGH and made explicit** in the metadata header and Quality gates,
   overriding the roadmap's "medium," because the content is patient-facing health material.
2. **"Questions, not answers" encoded in the schema** (no `answer`/`recommendation` field) — a
   structural, not just editorial, safety guarantee (Solution approach, Key decisions).
3. **Dual blocking sign-off** (oncology clinician *and* patient advocate) defined as two distinct
   mandatory disciplines, not interchangeable reviewers (Quality gates).
4. **Topic-appropriate reviewer rule** added for sensitive sets (palliative for end-of-life,
   genetic counsellor for hereditary, paediatric reviewer for paediatric) — set not shipped without it.
5. **Copyright trap addressed directly**: reference-only allow-list, original-authorship attestation,
   and the explicit point that a *selection/arrangement* of questions is itself protectable.
6. **AJCC staging carved out** as a copyrighted instrument we do not reproduce; we use public/generic
   staging vocabulary (Scope, Data/licensing).
7. **SEER/GLOBOCAN scoped to aggregate context only**, with controlled/identifiable data hard-excluded,
   matching the binding cancer guardrails (Data/licensing).
8. **Verified crisis/support-resource directory** made a first-class artifact with `verifiedDate`,
   and **required by CI** on any set touching distress/prognosis/end-of-life.
9. **Provenance-on-every-assertion** operationalized: any framing claim/rationale must cite a source
   and be clinician-endorsed, or be reworded to a pure question/dropped.
10. **Plain-language + accessibility** turned into measurable gates (reading-level target +
    a11y checks in CI + advocate sign-off), not aspirations.
11. **Agent uncertainty self-check** with a defined `UNCERTAIN:` format whose `advice-risk` type
    specifically targets the project's top hazard; unresolved flags block sign-off.
12. **Reviewer independence + COI declarations** required; the drafting human cannot be a sole reviewer.
13. **Reviewer disagreement resolution** with a "conservative reading wins" default (Quality gates).
14. **Definition of Shipped** distinguishes delivered (reviewed) vs done (adopted + given to patients),
    so review alone never counts as success.
15. **Outcome metrics, not vanity metrics**, with a small-sample reporting rule and a hard 0-critical-defect gate.
16. **Interim foundation metrics** added so progress is visible before reviewers/partner exist.
17. **Reviewer recruitment named as a blocking dependency** on par with securing a partner — a gap
    the exemplar's structure made easy to overlook for a high-risk project.
18. **Pause/decision points** for both missing reviewers (no sets built) and missing partner (go/pivot/hold).
19. **Source-change watcher** (hash/archive snapshots; M0 minimal, M1 automated) because clinical
    guidance changes — drift detection is foundation, not backlog.
20. **Review-refresh cadence** (`nextReviewDue` ≤12 months / on guideline change) with auto-flagging
    of stale sets and a withdrawal procedure (Sustainability).
21. **No-telemetry / no-patient-data** stance stated absolutely; partner patient feedback stays with
    the partner (only aggregate summaries reach Elyos) (Security & privacy).
22. **For-profit-steering guardrail**: no brands/drugs/sponsors; neutrality rubric + advocate review +
    refusal trigger (Risks, Quality gates).
23. **Content schemas added to `packages/schema`** (qplSet/qplQuestion/sourceAllowList/taxonomy/
    supportResource/review) with CI structural validation that fails on missing
    disclaimer/provenance/review/support — keeping validation agent-neutral.
24. **Translation deferred to a separate high-risk gate** (M3) reusing the `vital-info-translations`
    model, rather than smuggled into normal sets.
25. **Honest status** captured throughout: no proposal file yet, no reviewers, no partner;
    `verifiedNeed=false`; risk-tier reconciliation flagged as a governance open question.

---

## Review sign-off

**Reviewed for completeness against PLAN_SPEC (17 required H2 sections):** all present and in order —
Executive summary; Problem & beneficiaries; Goals and non-goals; Success metrics (outcomes); Scope;
Solution approach & architecture; Data, licensing & compliance; Quality, review & risk gates;
Roadmap & milestones; Work breakdown; Governance, roles & stakeholders; Dependencies & integrations;
Risks & mitigations; Security & privacy; Sustainability & maintenance; Open questions; References.

**Reviewed for correctness against the cancer guardrails (binding):**
- Open-access/aggregate/de-identified only — **PASS** (SEER/GLOBOCAN aggregate; controlled/identifiable
  data hard-excluded in Scope, Data/licensing, Risks).
- Per-source license verification — **PASS** (allow-list with `type`, snapshots, `verifiedBy/Date`;
  copyrighted sources reference-only; AJCC excluded).
- No medical advice; education-only + verbatim disclaimer + oncologist/advocate review (high) —
  **PASS** (questions-not-answers in schema; disclaimer on every artifact; dual blocking sign-off).
- Crisis/helpline info verified — **PASS** (verified directory artifact; CI-required on sensitive sets).
- Provenance on every assertion — **PASS** (provenance model; unsourced claims reworded/dropped).

**Fixes applied during review:**
- Reconciled the roadmap "medium" tag vs the high-risk reality by stating the **high elevation as a
  standing project decision** and adding it as a governance open question (#4).
- Made **reviewer recruitment an explicit blocking dependency** (not just the partner), with its own
  pause rule, after noticing the exemplar template foregrounds the partner but not reviewers.
- Added the **selection/arrangement copyright** nuance so "original questions" is not naively read as
  "any rearrangement is safe."
- Added a **CI requirement for support resources on sensitive sets** so the crisis-info guardrail is
  machine-enforced, not just policy.
- Noted **no proposal file exists** and added writing it as an open dependency (honest status).

**Outstanding human decisions (do not block planning, do block shipping):** secure credentialed
reviewers (oncology clinician + advocate); secure a partner; ratify the high risk-tier and write the
governance proposal; pin reading-level/accessibility targets and first region for support resources.

**Sign-off:** Draft v0.1.0 is internally consistent, schema-aligned, and guardrail-compliant; it is
ready for maintainer/governance review. It must **not** be used to ship any patient-facing set until
the blocking reviewer and partner dependencies are satisfied.
