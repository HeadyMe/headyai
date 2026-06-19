# HeadyAI — Claude Code Instructions

## REPO IDENTITY

**HeadyAI — Intelligence Routing Hub.** This repo serves the public-facing site
(`index.html`, `docs/`, `shared/`) deployed at the domain in `CNAME`. Treat it as
a production static site: keep markup valid, links live, `sitemap.xml`/`robots.txt`
consistent with published routes, and never introduce localhost or placeholder URLs.

## ARTIFACT CREATION CRITERIA

> **Standing bias: materialize durable work. Default to building the artifact, not pasting it inline.**

The most common failure mode is *under-production* — leaving a real deliverable
stranded in chat when it should have been written, committed, and registered.
When in doubt, build it. "Artifact" spans three senses; the bias applies to all.

### 1. Repo files & deliverables (primary)
Write to disk and commit — do **not** leave inline in the conversation — whenever
the output is **durable, reusable, or iterated on**:

- **Length/substance:** roughly **>15 lines** or larger than one screen.
- **Reuse:** anything that will be edited, run, saved, shared, or referenced again
  (pages, partials in `shared/`, docs, configs, scripts).
- **Iteration expected:** we'll revise it across turns — a file is a stable edit
  target; re-pasting is waste.
- **Self-contained deliverable:** complete page, component, doc, spec, or diagram.

Keep inline only: explanations, comparisons, answers to questions, and short
(<15-line) illustrative snippets relevant only in the moment.

### 2. Chat-surface artifacts (claude.ai / canvas / Slack canvas)
In UIs that render side-panel artifacts, promote substantial content (code,
documents, interactive previews) out of the message body using the same
length/reuse/iteration thresholds. For polished frontend/UI deliverables, use the
`artifact-design` skill rather than sketching inline.

### 3. Build/deploy artifacts
Built/published outputs (rendered pages, bundled assets) must be consistent and
discoverable — update `sitemap.xml` and internal links when pages are added or
moved. No orphaned outputs.

### Decision rule (all senses)
> If it is substantial, self-contained, and meant to be kept or reused — **build it
> and persist it**. If it is an explanation or a throwaway snippet — keep it inline.
