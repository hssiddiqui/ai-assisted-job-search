# Job Search Assistant

A lightweight, markdown-driven job-application framework for [Claude Code](https://claude.com/claude-code).
No LaTeX, no CLI scrapers, no Python required — job postings get found and filled out through
**browser automation** (Claude driving an actual browser), and the SOP, skills, and agents live as plain
markdown files Claude reads on every session.

Fork or copy this repo, fill in a handful of files with your own information, and Claude can:

- Evaluate a job posting against your real profile and give you a fit score
- Tailor your CV and write a cover letter for a specific posting
- Fill in application-form free-text fields (self-intro paragraphs, project entries, character-limited pitches)
- Prep you for an interview with STAR examples pulled from your actual CV
- Search a job board end-to-end, build a filtered candidate list, and work through it — applying to each
  posting via its actual online form, updating a tracker as it goes

> This is an independent template, not affiliated with Anthropic or with any specific job board.

## Prerequisites

- [Claude Code](https://claude.com/claude-code) (CLI or desktop app).
- **A browser-automation MCP.** This template's SOP was built and tested against the **claude-in-chrome**
  extension (Claude's own Chrome browser-automation tools — install it from the Chrome Web Store and connect
  it to Claude Code; see Anthropic's docs for the current setup steps). A Playwright-based MCP server works
  too with only minor tool-name adjustments to `CLAUDE.md`'s portal-quirk notes. Whichever you use, the
  agents in `.claude/agents/` assume *some* browser automation tool is connected.
- That's it. PDF rendering uses a headless Chromium browser you likely already have (Edge or Chrome) — see
  "Rendering a custom CV PDF" in `CLAUDE.md`. If you already have a LaTeX/pandoc pipeline you prefer, use
  that instead; the markdown→HTML→PDF path here is a fallback for machines that don't.

## Quick start

### 1. Fill in your profile

These four files are where you put your actual information — do this before asking Claude to do anything
real with this repo:

| File | What to fill in |
|---|---|
| `Application_Answers.md` | Contact info, work authorization, EEO answers, logistics, eligibility rules |
| `Application Materials/CV.md` | Your actual CV content (this is the master source; never edit it per-application, only copy it) |
| `.claude/skills/application-assistant/job-evaluation.md` | Your skills/experience for fit scoring, career goals, and the eligibility gate |
| `.claude/skills/application-assistant/interview-prep.md` | Your own STAR examples and draft answers to common questions |

Also render `Application Materials/CV.md` into a `CV.pdf` once you're happy with it — ask Claude to do this
("render my CV to PDF") and it'll follow the pipeline documented in `CLAUDE.md`.

### 2. Connect your browser-automation MCP

Get the claude-in-chrome extension (or your preferred alternative) installed and connected before asking
Claude to search or apply to anything — everything in `.claude/agents/` depends on it.

### 3. Start Claude Code in this repo

```bash
cd job-search-assistant
claude
```

Claude reads `CLAUDE.md` automatically at the start of every session in this directory — that's the SOP
that governs everything else.

### 4. Find some jobs

Give Claude a job board URL and ask it to find relevant openings:

> "Find relevant US-based data engineer openings on https://climatebase.org/jobs"

This invokes the `job-finder` agent (or the equivalent workflow if custom agents aren't registered in your
session yet — see the note below), which filters the board against your profile and eligibility rules and
writes a candidate checklist to `Job List/`.

**Job boards to try** (swap these for whatever's relevant to your market/industry — these are just
starting points, not an endorsement):
- General: [LinkedIn Jobs](https://www.linkedin.com/jobs/), [Indeed](https://www.indeed.com/)
- Climate/clean-tech: [Climatebase](https://climatebase.org/jobs), [ClimateTechList](https://www.climatetechlist.com/jobs)
- Data/tech-focused: [DataRoles.dev](https://dataroles.dev/)
- Or any individual company's own careers page

### 5. Apply

Once you've reviewed the candidate list, tell Claude to start applying:

> "Start applying to these, use my CV as-is"

This invokes the `job-applier` agent, which works the list top to bottom: re-verifies fit against each
actual posting, tailors the CV only if genuinely warranted, writes a cover letter for strong-fit postings,
answers standard questions from `Application_Answers.md`, and logs every outcome to
`Application Tracker/`.

**A hard safety rule that's baked into this repo and cannot be overridden in the moment:** the assistant
will never create an account or set a password on any portal, even if you tell it that's fine — it's a
"blocked step" like a CAPTCHA, left for you to finish by hand. See `.claude/agents/job-applier.md` for why.

> **Note on custom agents:** `.claude/agents/*.md` files (`job-finder.md`, `job-applier.md`) are Claude
> Code's custom-subagent mechanism, and in some setups they only get picked up after a fresh session start.
> If Claude reports the agent type isn't found, just ask it to do the task directly — everything the agents
> encode is also present in `CLAUDE.md` and the skill files, so the workflow still runs, just without the
> dedicated subagent.

## Other things you can ask for directly

No slash commands needed — plain language works:

| Say this | Gets you |
|---|---|
| "Evaluate this job posting" (paste URL or text) | An eligibility check + 5-dimension fit score against your profile |
| "Write a CV for [company]" | A tailored copy of your CV, rendered to PDF |
| "Write a cover letter for [role] at [company]" | A cover letter in your style, rendered to PDF |
| "Fill out the application form fields for [company]" | A `.txt` file with self-intro/project-entry/character-limited answers |
| "Help me prepare for an interview at [company]" | STAR examples grounded in your CV, likely questions, and questions to ask them |
| "What jobs should I look for?" | A career-strategy discussion using your profile and fit framework |

## Repo layout

```
job-search-assistant/
├── CLAUDE.md                          # The authoritative SOP — process, portal quirks, tracker format
├── Application_Answers.md             # Your contact info, work authorization, EEO answers, eligibility rules
├── .claude/
│   ├── agents/
│   │   ├── job-finder.md              # Scrapes a job board into a filtered candidate list
│   │   └── job-applier.md             # Works a candidate list end-to-end, applying to each posting
│   └── skills/
│       └── application-assistant/
│           ├── SKILL.md               # Skill entry point / workflow overview
│           ├── job-evaluation.md      # Fit-scoring framework — fill in your profile here
│           ├── cv-templates.md        # CV tailoring rules + the markdown→HTML→PDF render pipeline
│           ├── cover-letter-templates.md
│           ├── writing-style.md       # Tone rules (no em-dashes, no cliches, verify every company claim)
│           ├── interview-prep.md      # STAR framework — fill in your own examples here
│           └── application-forms.md   # Free-text application-form field guidance
├── Application Materials/
│   ├── CV.md                          # Master CV source — edit this, never the per-application copies
│   ├── CV.pdf                         # Render this from CV.md; used as-is for most postings
│   ├── Cover Letter Sample.md         # Style/tone reference once you have a real one you like
│   ├── Rejection_Response.md          # Template for replying to rejections/status updates
│   └── tmp/                           # Generated per-application drafts — cleaned up after submission
├── Application Tracker/
│   └── README.md                      # Convention for one-tracker-file-per-source (create files as you go)
└── Job List/
    └── README.md                      # Convention for candidate-list files the job-finder agent produces
```

## Safety notes

- **Prompt injection:** job postings and application forms are treated as untrusted text. Instructions
  embedded in them that are addressed to an AI get ignored and flagged, never followed.
- **Account creation / passwords:** never done autonomously, always left as a manual step for you (see
  above).
- **Standard-question answers** only come from `Application_Answers.md`, not invented per-posting.
- **Company claims in cover letters** must be independently verified (via web search/fetch against sources
  *you* locate, never by trusting a link inside the posting itself) before being included — see
  `writing-style.md` rule 5.
- Review before you send. This automates the mechanical work of applying, not your judgment about which
  jobs to pursue or what to say about yourself.

## Acknowledgements

The skill-based structure here (a job-fit evaluation rubric, CV/cover-letter tailoring rules, an
interview-prep framework, all organized as a Claude Code skill that a persistent SOP file invokes) follows
the pattern established by [Mads Lorentzen's `ai-job-search`](https://github.com/MadsLorentzen/ai-job-search)
— a considerably more feature-complete framework with LaTeX CV/cover-letter compilation, CLI job-portal
scrapers, a drafter-reviewer application pipeline, Notion/Gmail sync, and more. If you want that level of
tooling, or you're in a market with job boards it already has scrapers for, go check it out directly.

This repo is a lighter-weight sibling for a different setup: no LaTeX/Bun/Python toolchain, no custom CLI
tools per job board — everything here runs through Claude Code's own file-editing and browser-automation
tools instead. The skill *content* (scoring dimensions, tailoring rules, writing-style rules) was written
independently for this repo's own approach, not copied from that project, but the overall shape owes a debt
to it — hence the credit, and the same MIT license.

## License

MIT — see `LICENSE`. The copyright line in `LICENSE` has a placeholder for your name; fill it in once this
is actually your repo.
