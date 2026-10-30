# AI Proposal Triage Design

The example concerns a 150 kW warehouse rooftop solar project in Windsor,
Ontario, with a CAD 260,000 ceiling and completion within 16 weeks of award.

## 1. AI versus rules

The admin approves a versioned category configuration: mandatory predicates,
weights, evidence fields, scoring settings, project limits, and tie-breaks.
Code validates it, including weights totaling 100%. Criteria are configured
through admin screens; the application supplies reusable rule operators.

The reviewer uploads proposals and selects the category. Code validates file
type/size/page limits, converts PDF to text, and uses OCR when necessary. Poor
extraction is flagged. From the configuration, code builds a schema and prompt.
AI extracts facts and exact supporting quotes, one proposal per call; it never
scores or ranks. Code validates types, evidence locations, quoted text, units,
and consistency, and combines a document instruction scan with AI-reported
instruction findings. Invalid output gets one retry, then human review.

These handoffs produce three validated JSON stages: criteria, extracted facts,
and ranking. AI helps interpret variable language; rules handle arithmetic and
decisions that must be consistent. Store evidence before reviewer confirmation,
then apply mandatory checks, scoring, and sorting. Use templated explanations.

## 2. Consistency and explainability

Cache confirmed facts against the document hash and extraction versions.
Identical facts, criteria, scoring rules, and tie-breaks produce identical
results; fresh AI extraction is not guaranteed identical, even at temperature
zero. The reviewer sees each criterion's evidence, raw score, weight, and
contribution beside the ranking.

The following illustrative rubric is admin-approved before bids are evaluated.
Its anchors are design assumptions, not additional requirements from the brief.
Each raw score is 0–100; total = sum(raw score × weight/100).

| Criterion | Weight | Raw score |
| --- | ---: | --- |
| Experience | 30% | 100 × min(qualifying installs/10, 1) |
| Price | 25% | clamp(100 × (260000 − price)/65000, 0, 100) |
| Timeline | 15% | clamp(100 × (16 − weeks)/8, 0, 100) |
| Warranty | 15% | 50 × min(panel years/25, 1) + 50 × min(workmanship years/15, 1) |
| Team/approach | 15% | 25 each for named lead, crew size, safety plan, monitoring plan |

Thus full price marks begin at CAD 195,000 and full timeline marks at eight
weeks. Anchors, caps, checklist items, and limits are configuration values.

The bidder must confirm its own Ontario electrical contractor licence, WSIB
clearance, and CAD 5M liability cover. A confirmed mandatory failure is
`ineligible`. As an explicit project-policy assumption, exceeding either
budget or deadline is also ineligible. Unreadable or ambiguous evidence,
unresolved manipulation, missing schedule, or insufficient quantitative scoring
facts are `flagged`, with no rank or score. Missing optional team evidence earns
zero for that item. A sample's explicit named-lead claim earns that item without
inventing a person's name.

Experience qualifies only for commercial installs of at least 100 kW within
five years of the recorded evaluation date. For this worked example, assume
A's and E's reported counts qualify. This is not verified date-level evidence;
live ambiguity requires clarification.

Keep full calculation precision. Sort by unrounded score, then lower price,
shorter timeline, and proposal ID. Round the displayed total once to one decimal.
Adding another bid changes positions, not existing scores.

| Proposal | Experience | Price | Timeline | Warranty | Team | Total |
| --- | ---: | ---: | ---: | ---: | ---: | ---: |
| A | 30 | 8.461538… | 7.5 | 12.5 | 15 | 73.5 |
| E | 24 | 6.730769… | 5.625 | 13.5 | 15 | 64.9 |

A ranks first through higher experience, price, and timeline contributions;
E's stronger warranty does not offset them. Both earn full team points;
monitoring duration receives no extra points. B is ineligible because the
bidder does not confirm its own licence. C is flagged for instructions aimed
at manipulating automated review; these are ignored, and its experience period
also needs clarification before scoring. D is flagged pending a schedule.

## 3. Human oversight and audit

Five checkpoints: admin criteria approval; reviewer upload/category selection;
merged extraction-and-flags review; ranking review; final award by a named
person. At scale, review exceptions plus the top 10–20 results with full detail.

Only a reviewer can release a flag, with a written reason. Clarification stays
pending; exclusion is recorded as ineligible. Release reruns normal checks and
never waives requirements. Keep the detection and evidence. Record human
overrides separately from the original computed ranking.

Audit the file hash, text/extraction versions, facts and quotes, prompt/model,
criteria/scoring versions, evaluation date/run, scores, flags, every edit or
override with who/when/why, and the final decision. Fact corrections create a
new result version.

## 4. Changing criteria

An edit creates a new version. Reevaluate the comparison set under that version;
never mix versions in one ranking. Reuse sufficient saved facts for weight or
formula changes. New or changed evidence requirements, including an experience
window change, require targeted extraction/validation or clarification.
Preserve old results as superseded with a comparison view, reconfirm overrides,
and never silently change an awarded decision.

## 5. Risks and safeguards

- **Wrong extraction/hallucination:** explicit unknowns, schema and quote checks,
  unit validation, and reviewer confirmation. A matching quote does not itself
  prove the extracted interpretation or a contractor's claim is true.
- **Manipulation:** isolate untrusted text, combine scans and AI findings, and
  require logged human release. Detection can miss attacks; AI has no scoring
  or criteria-editing authority.
- **Bias:** use proposal IDs for scoring and the same approved rubric for all;
  inspect extracted evidence because name-blind arithmetic alone cannot remove
  extraction bias.
- **Cost/outage:** bounded uploads/output, cached facts, one retry, and manual
  fallback. Never silently drop a failed proposal or turn missing facts into
  passing results.
