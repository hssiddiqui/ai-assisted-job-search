---
name: application-assistant
description: >
  Assists with job applications: evaluating job postings, tailoring CVs, writing cover letters,
  filling application-form free-text fields, and preparing for interviews. Triggers on keywords
  like: job posting, job application, CV, cover letter, resume, interview prep, job fit, career,
  application, apply.
---

# Job Application Assistant

Extends the SOP in the repo's `CLAUDE.md`. This skill governs *content quality* (fit
scoring, tailoring, tone, interview prep); `CLAUDE.md` governs *process* (duplicate
checks, portal mechanics, tracker updates). Follow both — this file doesn't repeat
process steps that are already covered there.

**Writing style applies everywhere.** `writing-style.md`'s rules (no em-dashes, no
cliches, no unverified company claims, forward-looking framing) govern every piece of
prose this skill produces — cover letters, form answers, interview prep notes — and
should also shape how responses are written in this repo generally (status updates,
tracker notes), not just the documents listed below.

---

## Workflow

When the user provides a job posting (URL or text), follow this workflow:

### Step 1: Research & Evaluate Fit
- Fetch the job posting content (if URL) or read the text (if pasted)
- Analyze the posting for required competencies, keywords, and priorities
- Research the company (website, LinkedIn, mission, recent news) — see the Company
  Research Checklist in `job-evaluation.md`
- Score the posting against the candidate's profile using the framework in
  `job-evaluation.md` (includes the Eligibility Gate — run this first, it can short-
  circuit everything else)
- Present the evaluation table and verdict
- Suggest whether to call the employer before applying (see `job-evaluation.md`)
- Ask the user if they want to proceed

### Step 2: Tailor CV
- Derive a `<company>-<role>` slug once (lowercase, hyphenated, e.g. `acme-data-scientist`)
  and reuse it for every file this posting produces.
- Default to `Application Materials/CV.pdf` **as-is** per `CLAUDE.md` —
  only invoke this step when tailoring is clearly warranted (title mismatch, emphasis
  the generic summary doesn't cover).
- Copy `Application Materials/CV.md` (never edit the template itself),
  make minimal targeted edits per `cv-templates.md`.
- Render to `Application Materials/tmp/cv_<slug>.html` then
  `Application Materials/tmp/cv_<slug>.pdf` via the render pipeline in
  `cv-templates.md`.
- Visually inspect the rendered PDF before presenting (see `cv-templates.md`'s
  render-and-inspect loop).

### Step 3: Write Cover Letter
- Only if the posting requires or allows one (or proactively for a strong-fit posting —
  see `CLAUDE.md`).
- Follow `writing-style.md` and the structure in `cover-letter-templates.md`.
- Render to `Application Materials/tmp/cover_<slug>.pdf` via the same pipeline.

### Step 4: Application-Form Free-Text Fields
- If the portal asks for a self-introduction, structured project entries, or a
  character-limited pitch, follow `application-forms.md`.
- Output as `Application Materials/tmp/formfields_<slug>.txt`.

### Step 5: Interview Preparation
- Follow the framework in `interview-prep.md`.
- Prepare STAR-format answers, role-specific talking points, and questions to ask.

### Cleanup
- Once an application is confirmed submitted, delete the generated tmp files for that
  posting (`cv_<slug>.*`, `cover_<slug>.*`, `formfields_<slug>.txt`) — per `CLAUDE.md`,
  don't leave drafts sitting in the repo. Interview prep notes are the exception: keep
  those until after the interview.
- Update `Application Tracker/*.md` per `CLAUDE.md` step 7 — this skill doesn't
  maintain a separate tracking file.

---

## Reference Files

| File | Purpose |
|------|---------|
| `writing-style.md` | Tone, structure, do's and don'ts — applies to all prose this skill produces |
| `job-evaluation.md` | Eligibility gate + scoring framework for job fit — **fill in your profile here** |
| `cv-templates.md` | Markdown→HTML→PDF CV structure and tailoring rules |
| `cover-letter-templates.md` | Markdown→HTML→PDF cover letter structure and tailoring rules |
| `interview-prep.md` | STAR examples, tough questions, roleplay guidelines — **fill in your own examples here** |
| `application-forms.md` | Portal free-text fields: self-introduction, project entries, character-limited pitches |

---

## Quick Commands

You can also ask for individual steps without the full workflow:
- "Evaluate this job posting" — Step 1 only
- "Write a CV for [company]" — Step 2 only
- "Write a cover letter for [role] at [company]" — Step 3 only
- "Fill out the application form fields for [company]" — Step 4 only
- "Help me prepare for an interview at [company]" — Step 5 only
- "What jobs should I look for?" — career strategy discussion using the profile and
  evaluation framework in `job-evaluation.md`

No slash commands are needed — invoking this skill happens automatically from the
phrases above (or explicitly with `/application-assistant`).
