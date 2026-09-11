# CV Templates and Tailoring Guide

## Pipeline: Markdown → styled HTML → headless-browser PDF

If your machine has no LaTeX, no pandoc, and no LibreOffice, the pipeline documented in
the repo's `CLAUDE.md` ("Rendering a custom CV PDF") still works: build a styled HTML
file and render it with a headless Chromium-based browser. Do not attempt LaTeX,
pandoc, or Word automation unless you've set one of those up yourself and prefer it.

**Master source:** `Application Materials/CV.md` — read this for content,
but never edit it. Copy it, tailor the copy.

**Output files:** `Application Materials/tmp/cv_<slug>.html` and
`Application Materials/tmp/cv_<slug>.pdf`, where `<slug>` is the
`<company>-<role>` slug derived in `SKILL.md` Step 2.

**Render command** (per `CLAUDE.md`, adjust the browser path for your OS):
```bash
"C:\Program Files (x86)\Microsoft\Edge\Application\msedge.exe" ^
  --user-data-dir=<throwaway-temp-dir> --headless=new --disable-gpu --no-sandbox ^
  --no-pdf-header-footer --print-to-pdf="Application Materials/tmp/cv_<slug>.pdf" ^
  "file:///Application Materials/tmp/cv_<slug>.html"
```
Always use a throwaway `--user-data-dir` — the default profile may already be running
and silently swallow the command. Wait for the process to exit before reading the
output file.

### HTML/CSS structure

The first time you render a CV, design a clean resume layout and save it as the
reference (e.g. keep the first tailored HTML/CSS you're happy with as a model) — then
reuse that exact structure for every future tailored version rather than redesigning it
each time. A reasonable starting point:

- `@page { size: Letter; margin: 0.45in 0.6in; }`
- Body font: a serif font (Times New Roman / Times), 10.5pt, line-height ~1.18 — or
  whatever matches your default CV's look.
- `.header` block: centered doc title, name (17pt bold), contact line, links line.
- `h2` for section headings: 11pt bold, underlined, uppercase.
- `.entry-row` (flex, space-between, bold) for an org/employer line with location or
  dates on the right; `.entry-sub` (flex, space-between, italic) for the role title and
  date range under it.
- Standard `<ul>`/`<li>` for bullets; `<ol>` for a publications list if relevant.

The goal is visual consistency across every version presented to an employer — copy
your established structure rather than inventing a new layout per application.

### HTML escaping

The content source is plain Markdown/text, the target is HTML — escape:

| Character | Write |
|---|---|
| `&` | `&amp;` |
| `<` | `&lt;` |
| `>` | `&gt;` |

(`%`, `$`, `#`, `_` need no escaping in HTML — that's a LaTeX-only concern.)

## Section-by-Section Tailoring

### Profile Statement / Elevator Pitch (Best Practice)
The most important section to customize — the `SUMMARY (...)` heading and paragraph
right after the header.

Swap the role title in the heading (`SUMMARY (Data Analyst)` →
`SUMMARY (Data Scientist)`, etc.) and adjust which parts of the paragraph get
emphasized. Keep it 4-6 lines. Don't fabricate — every sentence must already be
supportable by the CV's own content.

When the role sits outside your home domain, **lead with the
domain-transfer argument** in the opening sentence — e.g. "statistical methods applied
to X" — rather than burying it in the cover letter.

### Skills Section (Best Practice)
Reorder your skill categories so the most relevant one to the posting comes first. Use
the posting's own term where truthfully applicable (e.g. its exact tool/framework name
over a paraphrase) — ATS and skim-reading hiring managers match literally.

### Education
Keep all degrees. If a degree is in progress, always state that explicitly (e.g. "Aug
2023-May 2027 (expected)") — a bare year range would misread as finished. Keep this
phrasing in every tailored copy; never quietly drop "(expected)".

### Professional Experience
Rewrite bullet emphasis, not facts, per posting. If any single role has many bullets
covering very different skills, pick and reorder the 4-6 most relevant to the
target role rather than using all of them every time.

**Tenure-vs-output check:** if a tailored version trims most of a long-tenure role's
bullets to fit space, make sure what remains doesn't make a multi-year role look thin.

### Selected Projects
Include the ones most relevant to the posting. If you have a project that's your
strongest signal for a specific role type (e.g. an AI/ML project for ML-adjacent roles),
it should rarely be cut regardless of which posting you're tailoring for.

### Selected Publications (if applicable)
For non-research roles, cut to the 2-3 most relevant or drop the section header down in
priority; for research-adjacent roles, keep most or all of them.

### References
Keep real contacts listed as-is — don't invent others, and don't list someone without
having actually asked them.

## Date fields (robustness note)

Write date ranges with a plain ASCII hyphen (`2023-Present`), not an en-dash character.
Some ATS portals still parse dates by splitting on a literal hyphen, and a
smart-quote/dash autocorrect from an editor can silently introduce a real en-dash
character. Check the rendered HTML source if a date range looks suspicious.

## Render-and-Inspect Loop (MANDATORY)

After rendering, before presenting to the user:

1. Confirm the PDF file was actually written (non-trivial size).
2. Read the PDF via the Read tool and visually inspect it.
3. Check: page count reasonable (matches your default CV's page count — a tailored
   version shouldn't balloon past that without a reason), no content clipped at page
   edges, no orphaned section headers with their content pushed to a new page, links
   intact.
4. If something looks wrong, fix the HTML/CSS and re-render — don't hand-adjust the PDF.

### Text-layer sanity (lighter than a LaTeX checklist)

A headless-Chromium PDF built from real HTML text keeps a clean, correctly-mapped text
layer by construction — the classic LaTeX failure modes (glyph-name garbage from
unmapped fonts, ligature-based date corruption) don't apply here. Two manual checks are
still worth doing:

- **Contact info as literal text, not only inside a link.** The email/phone in the
  header must appear as visible text, not carried solely by an `href`.
- **Keyword coverage.** Skim the rendered content against the posting's required/
  preferred terms and confirm the tailored version surfaces them.

Optional: if you install a PDF text-extraction library (e.g. Python's `pypdf`), you can
automate this check by diffing extracted PDF text against posting keywords. Not
required for normal use.

## Page Budget — Match the Default CV's Footprint

Use your default CV's page count as the target. As a rough per-section guide when
tailoring a 1-2 page CV:

| Section | Guidance |
|---------|----------|
| Summary | 4-6 lines |
| Skills | 3-4 categories, 1-2 lines each |
| Professional Experience | 3-6 bullets per role, weighted toward your most relevant/recent roles |
| Selected Projects | 1-3 entries depending on relevance |
| Education | All degrees |
| Publications (if applicable) | 3-6 depending on role relevance |

**If in doubt, cut rather than squeeze** — reducing margins or font size to force-fit
content looks cramped and inconsistent with your default CV's look.

## Relevance-weighted cutting (the right way to shrink a CV)

**Cut by signal, not by section.** A bullet that speaks directly to the posting is
worth more than a project entry that doesn't, regardless of which section
"normally" gets trimmed first.

For every candidate line, weigh:
1. **Relevance to THIS posting** — does it hit a named tool, keyword, or responsibility?
2. **Uniqueness** — is the claim made anywhere else in the CV?
3. **Narrative load** — does the cover letter lean on this line? If cutting it forces a
   cover-letter rewrite, it's load-bearing.

### Practical order of cuts
1. Redundancy between Skills and an Experience bullet — cut the Skills mention, keep
   the concrete bullet.
2. Low-relevance Selected Projects entries.
3. Low-relevance Professional Experience bullets, wherever they sit.
4. Low-relevance Publications (keep 1-2 that best match), if applicable.
5. Last resort: cut older/less-relevant education down to a single line, or drop the
   References section (rare — most portals don't need it in the CV since references are
   asked separately).

## Section Order

**Default (works for most roles):**
1. Summary
2. Education
3. Skills
4. Professional Experience
5. Selected Projects
6. Publications (if applicable)
7. References

**For roles where credentials matter more than recent output** (e.g. very
research-heavy postings): prioritize keeping full Education detail and trim Selected
Projects first, rather than reordering sections.
