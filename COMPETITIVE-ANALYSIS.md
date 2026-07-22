# Competitive & Improvement Analysis — `question-prompt-lists`

> Scope: rigorous review of `PLAN.md` (v0.1.0) + `TASKS.md` for the Hee-Lee Oss cancer good-deed project
> producing open, evidence-based "questions to ask your oncologist" prompt sets (QPLs) tagged by
> topic and journey stage. Web-researched, source-cited. CANCER GUARDRAILS apply throughout.

---

## 1. Correctness & completeness review of PLAN.md

The plan is unusually mature: it correctly elevates risk to HIGH, encodes "questions, not answers"
*structurally* (no `answer` field in the schema), gates on dual clinician + advocate sign-off,
handles the copyright trap (original authorship; reference-only allow-list; selection/arrangement is
itself protectable), excludes AJCC tables, scopes SEER/GLOBOCAN to aggregate-only, and is honest
that no reviewer/partner/proposal exists yet. Those are genuine strengths. The gaps below are real
and mostly concern the **evidence base** the plan claims but does not operationalize.

**G1 — The evidence base is asserted but not engineered into the design (most important finding).**
The plan repeatedly says QPLs are "well-studied" and "associated with greater question-asking and
recall," but never cites the literature and — more importantly — never absorbs its central, repeated
finding: **the benefit depends on the clinician actively endorsing/working through the QPL in the
consultation.** When oncologists explicitly addressed the prompt sheet, anxiety fell, consultation
time shortened, and recall improved; the QPL handed over passively does much less and can even raise
anxiety (Dimoska/Brown/Butow line of work, and the Clayton et al. 2007 palliative RCT, which paired
the QPL with physician endorsement)
([meta-analysis, PMC12391282](https://pmc.ncbi.nlm.nih.gov/articles/PMC12391282/);
[Clayton 2007 JCO RCT](https://ascopubs.org/doi/abs/10.1200/JCO.2006.06.7827);
[Promoting participation / shortening consultations RCT](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC2375236/)).
A pure static-content project that ships sets to patients without an accompanying **clinician-facing
"how to use this in clinic" companion** and a **patient-facing usage instruction** is shipping the
weak version of the intervention. This should be a first-class deliverable, not an omission.

**G2 — "QPL with instructions" beats "QPL alone," yet there is no patient usage-guidance artifact.**
Trials show adding brief instructions/coaching on how to use the list increases patient-initiated
questions and decision self-efficacy ([meta-analysis of RCTs](https://www.sciencedirect.com/science/article/pii/S2347562525001131);
[Brown coaching study](https://pubmed.ncbi.nlm.nih.gov/10390003/)). The schema has `introFraming`
but no explicit "how to use this list / it's OK to ask / bring a companion / ask the doctor to go
through it" guidance block. Add a structured `usageGuidance` element (and a clinician companion).

**G3 — Anxiety is named as a risk but the evidence is mishandled.** The plan lists "anxiety-inducing
content" generically. The literature is more specific and more actionable: QPLs can **transiently
increase anxiety immediately before/after the consult (especially prognosis/end-of-life prompts),
declining at follow-up**, and the moderator is physician endorsement
([advanced-cancer meta-analysis](https://pubmed.ncbi.nlm.nih.gov/38492095/)). The style guide should
encode evidence-based anxiety-mitigation (optionality framing — "questions you *may* wish to ask,"
permission-giving tone, sensitive-topic sequencing, signposting support lines adjacent to
prognosis/EoL questions), not just "avoid anxiety-inducing questions," which is too blunt and could
strip out exactly the prognosis questions patients most under-ask.

**G4 — Do not overclaim health outcomes.** Advanced-cancer meta-analyses find **no significant
improvement in anxiety, QoL, or survival** from QPLs; the robust effects are on *question-asking,
information recall, shared-decision engagement, and perceived helpfulness*
([PMC12391282](https://pmc.ncbi.nlm.nih.gov/articles/PMC12391282/)). The success metrics correctly
center "usefulness," but the Executive Summary / Problem framing should be tightened so the project
never implies clinical or psychological benefit it cannot evidence. The honest claim is a
**communication/empowerment** benefit.

**G5 — Reading-level + accessibility targets are deferred, but they gate every set.** The plan makes
readability/a11y a CI gate yet leaves the actual target as Open Question #5. M0's pilot set cannot
pass its own gate without a pinned target (e.g., a defined grade band, plus which a11y standard).
This is a sequencing error: pin the target in `qpl-style-001`/the schema, not "later." Also note
readability formulas (Flesch-Kincaid etc.) are weak for medical terms and non-English — the advocate
sign-off must remain the real bar, with the score advisory.

**G6 — Cultural/linguistic appropriateness is under-specified for v0.1.** The plan defers translation
(reasonable) but cultural framing is *not* the same as translation, and the cross-cultural QPL
literature shows direct lifts fail across cultures (the advanced-cancer QPL required cross-cultural
re-evaluation, e.g., the French ACP adaptation —
[JPSM French RCT](https://www.jpsmjournal.com/article/S0885-3924(20)30637-0/fulltext)). Even the
English v0.1 sets need a "cultural appropriateness" review dimension (already partly in the advocate
rubric) and should avoid US-only assumptions (insurance/cost framing, "second opinion" norms) so
sets are reusable internationally. Make `region`/`healthSystemAssumptions` an explicit set field.

**G7 — "Leading question" neutrality needs an operational test, not just a principle.** The schema
forbids answers, but a *question* can still lead ("Have you considered that surgery may be better
than radiation?"). The style guide should define concrete anti-patterns (no embedded comparative
claims, no presupposition of a clinically contested answer, no brand/modality steering) and the
CI/self-check should flag question text containing recommendation verbs or comparative claims. Right
now `advice-risk` and `leading` are flag *types* but there's no detection heuristic described.

**G8 — Metrics gaps.** (a) No metric for the **clinician-companion / endorsement** dimension despite
it being the efficacy driver (ties to G1). (b) "Patient/caregiver-reported usefulness — Positive
from a partner sample" has no threshold or instrument; consider a validated item (e.g., perceived
helpfulness vs. a usual information sheet, which is how trials measured it). (c) No metric for
**reach/equity** (did low-health-literacy / non-English-ready users actually get usable sets) — the
stated priority beneficiaries. (d) "0 critical defects" is good but undefined-denominator; specify
it's per-published-set and time-bounded.

**G9 — Minor/correctness.** (a) GLOBOCAN/IARC terms: the plan hedges "often non-commercial" — IARC
publications are frequently CC BY-NC, which would **conflict with CC BY 4.0 reuse** if any GLOBOCAN
text/figures are adapted; the allow-list must resolve this before any GLOBOCAN-derived framing ships
(safer: cite as reference, don't adapt). (b) SEER is public domain (citation requested) — correct.
(c) NCI/PDQ public-domain claim is correct but the per-page trademark/embedded-media caveat is real;
keep it. (d) The plan says copyrighted sets are reference-only "to verify which topics matter" —
note that even *deriving the topic taxonomy* from a single copyrighted source's structure risks a
selection/arrangement claim; ground the taxonomy in *multiple* sources + public PDQ structure to be
safe (the plan gestures at this; make it explicit in `qpl-taxonomy-001`). (e) Roadmap "medium" vs
plan "high" risk reconciliation is correctly flagged as Open Q#4 — keep it blocking.

**Completeness:** all 17 spec sections present. The missing *deliverables* are the clinician-use
companion (G1), patient usage guidance (G2), and a pinned readability/a11y/cultural spec (G5/G6).

---

## 2. Competitive landscape (real competitors / adjacent)

**NCI — "Questions to Ask Your Doctor About Cancer" (cancer.gov).** Topic/stage-segmented question
pages: diagnosis, treatment, advanced cancer, post-treatment/survivorship
([treatment](https://www.cancer.gov/about-cancer/treatment/questions),
[diagnosis](https://www.cancer.gov/about-cancer/diagnosis-staging/questions),
[advanced](https://www.cancer.gov/about-cancer/advanced-cancer/questions),
[finished treatment](https://www.cancer.gov/about-cancer/coping/survivorship/questions)).
*Strengths:* authoritative, **US public domain (reusable)**, already stage-organized, trusted brand.
*Weaknesses:* English-only, HTML/PDF (not machine-readable/structured data), no per-question
provenance/metadata, generic (not type-specific), no usage instructions or clinician companion, not
maintained as adaptable open data. **This is simultaneously the strongest competitor and the project's
best lawful source.**

**ASCO / Cancer.Net "Questions to Ask the Health Care Team."** Embedded in oncologist-approved,
type-specific guides; reviewed by a multidisciplinary editorial board including patient advocates
([Cancer.Net editorial model](https://pmc.ncbi.nlm.nih.gov/articles/PMC2793912/)).
*Strengths:* clinically vetted, type-specific, broad coverage, exactly the dual clinician+advocate
review model Hee-Lee Oss proposes — proven at scale. *Weaknesses:* **copyrighted (reference-only)**,
English-centric, embedded in long guides (not standalone structured QPLs), not openly licensed for
clinics/translators to adapt.

**American Cancer Society — "Questions to Ask When You've Been Diagnosed."** Includes printable
worksheets per type
([ACS diagnosis questions](https://www.cancer.org/cancer/managing-cancer/making-treatment-decisions/questions-to-ask-your-doctor.html);
[ACS PDF worksheet](https://www.cancer.org/content/dam/cancer-org/cancer-control/en/worksheets/questions-to-ask-about-my-cancer.pdf)).
*Strengths:* patient-friendly, printable, type-specific, well-known. *Weaknesses:* copyrighted,
static PDFs, English-first, not structured/adaptable.

**Macmillan Cancer Support (UK).** Question pages + the "Ask about your cancer treatment" booklet,
plus a phone support line
([Macmillan questions](https://www.macmillan.org.uk/cancer-information-and-support/treatment/your-treatment-options/questions-to-ask-your-healthcare-team)).
*Strengths:* strong plain-language/tone, integrated human support line, type-specific (e.g.,
lymphoma). *Weaknesses:* copyrighted, UK-health-system-specific, PDF/HTML, English.

**Cancer Research UK.** "What to ask your doctor," including a dedicated **rare cancers** page
([CRUK rare cancers](https://cancerresearchuk.org/about-cancer/rare-cancers/getting-diagnosed/what-to-ask-your-doctor)).
*Strengths:* good rare-cancer angle (relevant to Hee-Lee Oss's Ewing/sarcoma ties). *Weaknesses:*
copyrighted, UK-specific, static.

**AHRQ QuestionBuilder (app + web).** The closest *tool* competitor: a dynamic question-builder that
lets patients select/customize questions by appointment type and export to calendar/email; backed by
the "Questions Are the Answer" campaign
([QuestionBuilder](https://www.ahrq.gov/questions/question-builder/index.html);
[online version](https://www.ahrq.gov/questions/question-builder/online.html)).
*Strengths:* **interactive/personalized, exportable, US-government (public)**, evidence-informed.
*Weaknesses:* **general medical, not cancer/stage-specific**, no oncology depth, no per-question
sourcing, an app (not open adaptable content), English. **Strong integration target, not a rival.**

**The academic QPL literature (Butow, Brown, Clayton, Dimoska, Walczak).** The intervention's
evidence base: original Butow 1994 QPL; Brown coaching RCT
([1999](https://pubmed.ncbi.nlm.nih.gov/10390003/)); Clayton et al. palliative/EoL RCT
([2007 JCO](https://ascopubs.org/doi/abs/10.1200/JCO.2006.06.7827)); palliative QPL development
([BJC](https://www.nature.com/articles/6601380)); multiple meta-analyses
([general RCT meta-analysis](https://www.sciencedirect.com/science/article/pii/S2347562525001131);
[advanced cancer](https://pubmed.ncbi.nlm.nih.gov/38492095/);
[implementation into routine care](https://pubmed.ncbi.nlm.nih.gov/21741195/)).
*Strengths:* gold-standard validated question sets and effect evidence. *Weaknesses:* locked in
journals (often paywalled/copyrighted), not consumer artifacts, not maintained/translated, not
openly licensed. **This is the credibility backbone the plan currently under-uses.**

**Patient advocacy / community guides — Smart Patients, OncoLink, PatientPower, disease foundations.**
OncoLink (Penn, since 1994; 200+ experts; patient/family education center)
([OncoLink education center](https://www.oncolink.org/healthcare-professionals/o-pro-portal/patient-family-education-center));
Smart Patients (100+ moderated disease communities; ad-free)
([PanCAN x Smart Patients](https://pancan.org/press-releases/pancreatic-cancer-action-network-collaborates-with-smart-patients-to-launch-online-community-for-pancreatic-cancer-patients-and-caregivers/)).
*Strengths:* trusted, expert-vetted (OncoLink), lived-experience question sourcing (communities).
*Weaknesses:* copyrighted/community-owned, not structured open QPL data, English, not stage-tagged
as reusable datasets.

**Net:** every incumbent is some combination of **copyrighted, English-only, static (PDF/HTML/app),
not machine-readable, not openly adaptable, and not per-question sourced.** No one ships open,
structured, stage×topic-tagged, provenance-bearing, translation-ready QPL *data*.

---

## 3. Gaps we can fill

1. **Open + adaptable.** Incumbents are copyrighted or app-locked; clinics/charities/translators
   can't legally remix them. CC BY 4.0 original QPL data is a genuinely empty niche.
2. **Structured & machine-readable.** Stage×topic-tagged YAML/JSON with per-question metadata,
   provenance, sensitivity flags — vs. everyone else's PDFs/HTML. Enables filtering, rendering,
   translation, and tool integration.
3. **Per-question provenance.** No incumbent attaches source+version to each framing claim; this is
   a differentiator for trust, currency, and lawful reuse.
4. **Translation-ready by construction.** Incumbents are English-first; structuring for localization
   from day one (with a high-risk translation gate) addresses the stated language-barrier beneficiary.
5. **Health-system-agnostic framing.** NCI/ACS = US; Macmillan/CRUK = UK. A `region`/
   `healthSystemAssumptions`-aware design can serve both and the rest of the world.
6. **The under-served slices:** rare cancers (CRUK aside, thin), caregiver-specific variants,
   low-health-literacy and short-visit/community-clinic versions — all in the backlog, all gaps.
7. **The missing connective tissue:** a **clinician-use companion + patient usage guidance** (the
   evidence-based efficacy driver) that none of the static incumbents package with their lists.

---

## 4. Differentiators to win

- **Open, structured, provenance-bearing QPL *data* (CC BY 4.0)** — the single strongest, defensible
  differentiator: the only freely-remixable, machine-readable, stage×topic-tagged QPL corpus.
- **Evidence-faithful design**, not just evidence-cited: ships the *with-endorsement / with-instructions*
  version the trials show actually works (clinician companion + patient usage guidance).
- **Dual clinician + advocate sign-off with recorded COI** — matches ASCO's proven editorial bar but
  in the open, with the review block as structured, auditable data.
- **Provenance + license discipline as machine-checked CI gates** — trust you can verify, not assert.
- **Built for equity from v0.1** — plain-language target, accessibility, cultural-appropriateness
  review, translation-readiness aimed squarely at the most underserved patients.
- **Currency guarantee** — `nextReviewDue` + source-change watcher; incumbents' PDFs silently rot.
- **Composable** — integratable into AHRQ QuestionBuilder-style tools, EHR patient portals, or an MCP
  server, because it's data, not a destination site.

---

## 5. Claude API leverage

**Where Claude clearly helps (all human-/expert-gated):**
1. **Drafting topic/stage-specific original question sets** from allow-listed public-domain sources
   (NCI/PDQ, SEER context), grouped by topic, with `UNCERTAIN:` self-flagging — accelerating the
   author step in the pipeline while keeping output as *draft* for expert review.
2. **Plain-language + reading-level rewriting** to the pinned grade band, and surfacing jargon, long
   sentences, and presupposition/leading phrasing for advocate review (Claude as a first-pass
   readability + neutrality linter, score advisory).
3. **Translation drafting + back-translation QA** under the M3 high-risk gate (Claude drafts;
   qualified medical-translation reviewer + back-translation + clinician meaning-preservation
   endorsement decide) — exactly the `vital-info-translations` model.
4. **Non-clinical personalization-by-topic/stage**: assembling/sequencing the right *questions* for a
   selected cell (e.g., newly-diagnosed × clinical-trials × caregiver), tone/sensitivity adaptation,
   and generating the clinician-companion and patient usage-guidance text (G1/G2).
5. **Provenance/structure tooling**: drafting allow-list entries, normalizing YAML to schema,
   diffing re-fetched sources for the change-watcher, generating coverage-matrix reports.
6. **Leading-question detection heuristic** (G7): Claude as a CI check flagging recommendation verbs,
   comparative claims, and embedded answers in question text — advisory, expert-confirmed.

**Where Claude must NOT decide (hard guardrails):**
- **No answers, recommendations, prognoses, or interpretation** of a patient's situation — ever; the
  schema has no answer field and Claude must not smuggle implied answers into question wording.
- **Questions must be non-leading and clinically accurate** — final neutrality/accuracy is the
  **clinician + advocate** call, not the model's; no sign-off while any `UNCERTAIN:` flag is open.
- **No unsourced or fabricated claims** in framing/rationale — every assertion needs allow-listed
  provenance; the meta-analysis nuance (G3/G4) means Claude must not invent benefit claims.
- **No copyrighted-QPL reproduction** — Claude must author originals, never paraphrase-launder ACS/
  ASCO/NCCN/Macmillan/CRUK wording or their selection/arrangement.
- **No anxiety-inducing or alarmist content**; sensitive sets (prognosis/EoL/fertility/genetics)
  require the topic-appropriate human reviewer and verified support resources — model output is never
  the gate.
- **No PII / no controlled-access data**; aggregate/open only.

---

## 6. Ten concrete optimizations

1. **Add a clinician-use companion deliverable** ("how to introduce and work through this QPL in
   clinic") per set — operationalizes the endorsement effect that drives all measured benefit (G1).
2. **Add a `usageGuidance` block + patient instruction** ("these are questions you *may* wish to ask;
   it's OK to ask the doctor to go through them; bring someone") — the "QPL+instructions" uplift (G2).
3. **Pin readability + accessibility + cultural targets in M0** (in `qpl-style-001`/schema), since the
   pilot set can't pass its own gate otherwise; keep the score advisory, advocate sign-off binding (G5).
4. **Encode evidence-based anxiety-mitigation in the style guide**: optionality/permission framing,
   sensitive-topic sequencing, support-line adjacency for prognosis/EoL prompts (G3).
5. **Add a `region`/`healthSystemAssumptions` field** and a cultural-appropriateness rubric dimension
   so sets aren't silently US-only and are reusable internationally (G6).
6. **Ship machine-readable + multi-format renders** (printable, large-print, screen-reader, plain
   Markdown) from the structured source — the structured-data advantage incumbents lack.
7. **Build a leading-question CI linter** (recommendation verbs, comparatives, presupposition,
   embedded answers) as an automated first pass feeding `agentFlags` (G7).
8. **Cite the QPL evidence base in PLAN + each set's rationale** and add an `evidenceBasis` reference
   so the "why this works (for question-asking/recall, not health outcomes)" claim is grounded (G1/G4).
9. **Add reach/equity + endorsement metrics** (low-literacy/non-English usability; whether partner
   clinicians endorsed the QPL) and a validated "helpfulness vs. usual sheet" usefulness item (G8).
10. **Resolve GLOBOCAN/IARC licensing explicitly** in the allow-list (CC BY-NC conflicts with CC BY
    4.0 reuse) — prefer reference-only citation over adapting GLOBOCAN text/figures (G9a).

---

## 7. Parallel & perpendicular spin-offs

- **Generalized, condition-agnostic QPL engine.** The schema, style guide, review rubric, provenance
  model, and CI gates are disease-neutral. Spin out a core QPL framework that other conditions
  (diabetes, mental health, rare disease) reuse — cancer is the first vertical. High leverage.
- **AHRQ QuestionBuilder integration.** Contribute Hee-Lee Oss's open, sourced oncology question sets as
  content into the AHRQ tool flow (or mirror its export model) — partnership, not competition
  ([QuestionBuilder](https://www.ahrq.gov/questions/question-builder/index.html)).
- **MCP server for QPLs.** Expose the open corpus via an MCP server (`get_questions(stage, topic,
  cancerType, region, readingLevel)`) so any agent/portal can surface vetted, sourced questions —
  the composable, data-not-destination differentiator made real. (Read-only; carries disclaimers;
  no personalization that crosses into advice.)
- **Ties to sibling Hee-Lee Oss projects:**
  - `ewing-family-guide` / sarcoma: rare-cancer QPL sets (newly-diagnosed, second-opinion, trials),
    where incumbent coverage is thinnest (CRUK aside).
  - `ewing-trial-finder`: a dedicated **clinical-trials** QPL ("questions to ask about a trial:
    eligibility, randomization, phase, cost, travel") pairs naturally with trial discovery —
    questions-not-answers keeps it safe.
  - `survivorship-resources`: survivorship/post-treatment QPL sets (late effects, surveillance,
    return-to-work) reusing NCI's public-domain survivorship questions as source.
  - `nutrition-during-treatment`: a side-effects/supportive-care QPL ("questions to ask your
    dietitian/team about eating during treatment") — strictly questions, no nutrition advice.
- **Caregiver QPL line** (already in backlog) — distinct audience framing; caregivers ask different
  questions, well-supported by the EoL caregiver QPL literature
  ([caregiver EoL prompt sheet](https://pubmed.ncbi.nlm.nih.gov/18843134/)).
- **"QPL effectiveness" open dataset/registry** — a small structured index of the QPL RCT evidence
  (effect on question-asking, recall, anxiety, the endorsement moderator) used to ground claims and
  shareable as its own open artifact.

---

## 8. Open questions for the maintainer

1. **Will the project ship the evidence-faithful version?** i.e., commit to a clinician-use companion
   + patient usage guidance per set (G1/G2), or knowingly ship the weaker static-handout form?
2. **Readability/a11y/cultural targets** — pin the exact grade band, a11y standard, and whether a
   cultural-appropriateness review dimension is mandatory for v0.1 English sets (G5/G6).
3. **Region scope for v0.1** — US-first (NCI/SEER, cost framing) or health-system-agnostic from the
   start? This drives source mix, support-line directory, and partner choice.
4. **Anxiety/sensitive-content stance** — does the style guide *retain* prognosis/EoL questions (which
   patients most under-ask) with mitigation, rather than stripping them as "anxiety-inducing"? (G3)
5. **GLOBOCAN/IARC** — confirm reference-only (no adaptation) to avoid CC BY-NC vs CC BY 4.0 conflict;
   is SEER-only sufficient for any needed aggregate context? (G9a)
6. **Taxonomy provenance** — will the topic×stage taxonomy be grounded in *multiple* sources + public
   PDQ structure to avoid a selection/arrangement copyright claim? (G9d)
7. **MCP / integration appetite** — is an MCP server or AHRQ-integration in scope post-v0.1, given it
   amplifies the open-data differentiator?
8. **Evidence metric** — will the project track the *endorsement* and *equity/reach* dimensions, not
   just adoption counts? (G8)
