# AI Proposal Triage Design

- **Candidate:** Syed Muhammad Ashar Ali Rizvi
- **Reference:** MATACS-TH-2026-02
- **Time actually spent:** 1 hour 30 minutes
- **Repository:** [matacs-th-2026-02](https://github.com/AsharAli-042/matacs-th-2026-02)

This submission designs a contractor-proposal review process. AI extracts facts
and supporting evidence; configured rules determine eligibility, scores, and
rankings. A human makes the award decision. It is a design submission, with no
application deployment or prototype required.

## Files

| File | Contents |
| --- | --- |
| [README.md](README.md) | Candidate details, submission guide, and AI-use disclosure |
| [WRITEUP.md](WRITEUP.md) | Answers to the five questions, scoring rubric, assumptions, and sample results |
| [PROMPTS.md](PROMPTS.md) | Exact system/user extraction messages and clearly marked runtime inputs |
| [ranking.json](ranking.json) | Expected outcomes for proposals A–E in the requested format |
| [diagram/process-flow.png](diagram/process-flow.png) | Process-flow diagram showing human checkpoints, AI extraction, rules, and outcome branches |
| [.gitignore](.gitignore) | Excludes local source material, planning records, and credentials |

The landscape diagram groups inputs, extraction, review, and outcomes, from
approved criteria and proposal upload through the final human award decision.

## Reading the results

A ranks first at **73.5**, followed by E at **64.9**. C is held for manipulation
review, D needs a completion schedule, and B fails the bidder-licence requirement.
Unranked proposals have null ranks and scores. The worked example explicitly
assumes A's and E's reported experience counts meet the five-year requirement;
this assumption is explained in the write-up rather than presented as verified
installation dates.

## AI-use disclosure

I researched the approach and supplied the finalized design plan that forms
the basis of this submission. I used OpenAI Codex to review that plan against
the brief, refine edge-case handling, draft the submission documents and
extraction prompts, create the process-flow diagram, and verify scoring
arithmetic. During review, I challenged
the AI-generated PROMPTS.md for including unnecessary schema-generation
documentation and requested a simpler presentation of the actual system and
user messages to match the brief's prompt requirement more directly.

Only proposal letters and derived design/results are included; the source brief
and original proposal text are excluded. No live extraction model was run for
this submission, and no software implementation is claimed.
