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
| [PROMPTS.md](PROMPTS.md) | Exact extraction prompt templates, schema construction, and validation contract |
| [ranking.json](ranking.json) | Expected outcomes for proposals A–E in the requested format |
| [diagram/](diagram/) | Process-flow diagram; separate diagram export is pending |
| [.gitignore](.gitignore) | Excludes local source material, planning records, and credentials |

The diagram will be exported separately as `diagram/process-flow.png` (or one
JPG/PDF instead). Until that artifact is present, the submission is incomplete.

## Reading the results

A ranks first at **73.5**, followed by E at **64.9**. C is held for manipulation
review, D needs a completion schedule, and B fails the bidder-licence requirement.
Unranked proposals have null ranks and scores. The worked example explicitly
assumes A's and E's reported experience counts meet the five-year requirement;
this assumption is explained in the write-up rather than presented as verified
installation dates.

## AI-use disclosure

I used OpenAI Codex to help analyze the brief, refine the workflow, draft the
documentation and extraction prompts, and check scoring arithmetic. I reviewed
the suggestions and accepted a correction to the initial claim that every
criteria change could reuse cached facts without another AI call: changing an
experience window can require additional evidence, so the design now checks
whether the saved facts are sufficient. I also accepted an explicit
worked-example assumption for A's and E's five-year experience counts instead
of presenting their broad date ranges as verified qualifying experience.

Only proposal letters and derived design/results are included; the source brief
and original proposal text are excluded. No live extraction model was run for
this submission, and no software implementation is claimed.
