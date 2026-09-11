# Cover Letter Templates and Tailoring Guide

## Pipeline: Markdown → styled HTML → headless-browser PDF

Same toolchain as `cv-templates.md` — no LaTeX or Word automation required. Build a
styled HTML file, render it with a headless browser.

**Style reference:** `Application Materials/Cover Letter Sample.md` — once you have one
real prior cover letter you're happy with, use it for structure and tone,
not content — the specifics in it were tailored to that posting.

**Output file:** `Application Materials/tmp/cover_<slug>.pdf` (`<slug>` per
`SKILL.md` Step 2).

**Render command:** same as `cv-templates.md` — headless browser with a throwaway
`--user-data-dir`, `--print-to-pdf`.

### HTML/CSS structure

A clean sans-serif body (Arial/Helvetica) reads as intentionally
distinct from a serif CV — keep that contrast if your CV uses a serif font. A simple
structure:

- `@page { size: Letter; margin: 1in; }`
- Body font: Arial / Helvetica / sans-serif, 11pt, line-height ~1.3.
- Header: name, contact line (email, phone, LinkedIn), right- or left-aligned.
- Date line.
- Salutation, then plain `<p>` paragraphs — no bullet list by default (see below).
- Closing + signature name.

## Document Structure (default)

Flowing paragraphs with **bolded inline category labels**, each tied to a posting
requirement, tend to read better than a bulleted list:

```
Dear [Name],

I am writing to express my interest in the [Role] position at [Company]. [1 sentence
connecting background/how you found the role to this posting.]

Here's why I believe I am a great fit for this position:

[Category Label 1]: [1-2 sentences connecting a specific experience/skill to this
requirement.]

[Category Label 2]: [1-2 sentences.]

[Category Label 3]: [1-2 sentences.]

[Category Label 4 — optional, 3-5 total]: [1-2 sentences.]

Thank you for your consideration. I look forward to discussing how [1 forward-looking
sentence tying background to what the employer needs].

Best,
[Your Name]
```

**Illustrative example** (labels are per-posting, not a fixed set to reuse verbatim —
pick 3-5 from what the posting actually asks for): a posting emphasizing domain
expertise, technical depth, analytical skills, and communication might use labels like
"Domain Expertise," "Technical Depth," "Data Analysis Skills," and "Research &
Communication" — each chosen because it maps directly onto something in that specific
posting.

### Bullet-list alternative

For a posting where a scannable list reads better (e.g. a very keyword-driven ATS
posting, or a shorter/less formal letter), a bulleted variant is fine:

```
Dear [Name],

[Opening paragraph.]

[Body paragraph introducing the list.]

<ul>
  <li><strong>[Label]:</strong> [achievement/skill]</li>
  <li><strong>[Label]:</strong> [achievement/skill]</li>
  <li><strong>[Label]:</strong> [achievement/skill]</li>
</ul>

[Company-specific paragraph.]

[Closing.]

Best,
[Your Name]
```

Default to the prose-with-bold-labels form unless there's a specific reason to prefer
the list.

## Tailoring Guidelines

### Salutation
- If the hiring manager's name is known: "Dear [First Last],"
- If only the team is known: "Dear [Company] hiring team,"
- Generic: "Dear [Company]," (avoid "To whom it may concern")

### Length — Hard 1-Page Limit
- Target: 1 page including signature.
- **Word budget: 250-300 words** of body text. 350 will overflow.
- Count: opening + 3-5 labeled segments + closing. Add a company-specific paragraph
  only if the rest is short enough to absorb it.

### HTML escaping
Plain text source, HTML target — escape `&` → `&amp;`, `<` → `&lt;`, `>` → `&gt;`.

### Non-English cover letters
If you're applying outside an English-language market, adapt tone/structure rules to
that language's professional conventions — the structural skeleton above still applies,
but salutation/closing conventions vary by country.

## Render-and-Inspect Loop (MANDATORY)

Same as `cv-templates.md`:
1. Render via headless browser.
2. Read the resulting PDF and visually confirm: exactly 1 page, signature fits at the
   bottom, no text clipped, no leftover placeholder text.
3. Fix the HTML and re-render if anything is off.

## Checklist Before Finalizing
- [ ] No em-dashes (use commas or periods instead)
- [ ] No cliches or empty filler
- [ ] Every claim backed by a specific, verifiable example
- [ ] Forward-looking framing: focuses on tasks solved, not just past duties
- [ ] Company-specific paragraph references this company's mission/values/recent work,
      each claim independently verified per `writing-style.md` rule 5
- [ ] Company name and role are correct throughout
- [ ] Date is current
- [ ] Fits on exactly 1 page
- [ ] Salutation is appropriate (named person if possible)
- [ ] Rendered PDF visually inspected (not just the HTML source)

## Submission Guidelines
- Submit only the documents the employer requests.
- Export as PDF — some portals (e.g. governmentjobs.com/NEOGOV) reject non-PDF uploads.
- Delete `cover_<slug>.html`/`.pdf` once the application is confirmed submitted, per
  `CLAUDE.md`.
