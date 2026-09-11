# Job Evaluation Framework

**Fill in every bracketed section below with your own situation before using this skill for real.** The
scoring mechanics (dimensions, weighting, thresholds) are ready to use as-is; the *content* of each dimension
needs to describe you.

## Eligibility Gate — run before scoring

Read `Application_Answers.md`'s Work Authorization section, then classify the posting:

| Posting wording | Verdict |
|-----------------|---------|
| Requires a citizenship/status you don't hold, or a security clearance you don't hold or can't get | **FAIL — hard stop.** Do not score, do not draft. Quote the exact wording back to the user. |
| Names a specific company on your blanket-skip list (see `Application_Answers.md` Notes section — add
  companies there as you confirm them, e.g. an employer with an ITAR/US-person requirement) | **FAIL — hard
  stop**, regardless of the specific posting's wording. |
| Contains an export-control clause you don't clear (e.g., in the US, nuclear-sector postings often cite
  **10 CFR Part 810 Appendix A** — whether this disqualifies you depends on your citizenship/residency
  status; check `Application_Answers.md`) | **FAIL — hard stop** if your `Application_Answers.md` says this
  applies to you. |
| Anything else — sponsorship-related language, "must be authorized to work in [country]", silent on
  citizenship | **PASS**, assuming your own `Application_Answers.md` work-authorization answers clear it. |

A role that fails this gate is not scored and not drafted. Everything below applies
only to roles that pass it.

**Experience-years requirements**: [State your own policy here — e.g. does research/lab work, a bootcamp, a
freelance stretch, or military service count toward a posting's "N+ years" ask? Don't screen out an
otherwise-relevant posting on that basis alone if it should count. This does not cover qualitative bars
unrelated to tenure (e.g. "must have shipped production systems with real users") — those are still real
gaps to flag.]

## Scoring Dimensions

Evaluate each job posting against these five dimensions:

### 1. Technical Skills Match (0-100)
How well do the required/preferred skills align with the candidate's capabilities?

| Score | Meaning |
|-------|---------|
| 80-100 | Core requirements are primary skills |
| 60-79 | Most requirements match, 1-2 gaps that are learnable |
| 40-59 | Partial match, significant upskilling needed |
| 0-39 | Fundamental mismatch |

**Strong match areas:** [List 3-6 skills/tools/domains you're genuinely strong in — the ones that should
score 80-100 when a posting asks for them.]

**Moderate match areas:** [List skills you have working familiarity with but aren't your core strength.]

**Weak match areas:** [List categories of work you're clearly not suited for right now, so the evaluation
can flag a fundamental mismatch quickly instead of over-scoring a bad fit.]

### 2. Experience Match (0-100)
Does work history align with what they're looking for? Match on the function and nature
of the work performed, not the literal job title — two differently-titled roles can be
functionally identical.

| Score | Meaning |
|-------|---------|
| 80-100 | Direct experience in the same domain and role type |
| 60-79 | Related experience, transferable skills clear |
| 40-59 | Adjacent experience, would need to make the case |
| 0-39 | Unrelated experience |

**Strong:** [List the roles/projects/domains from your background that map most directly onto the kind of
work you're targeting.]

**Moderate:** [List adjacent experience that's a reasonable but not perfect match.]

**Entry-level territory:** [Note honestly where your experience is thinner than what some postings will ask
for, and which specific projects/roles are your best evidence to lean on there.]

### 3. Behavioral/Culture Fit (0-100)
Does the role and company culture match your behavioral preferences?

| Score | Meaning |
|-------|---------|
| 80-100 | Culture strongly matches behavioral preferences |
| 60-79 | Mixed signals but mostly compatible |
| 40-59 | Some friction areas |
| 0-39 | Significant culture mismatch |

**Red flags to research:** Department disorganization, work dominated by maintenance
over development, poor chemistry with leadership, culture mismatches. Check reviews,
media coverage, LinkedIn connections, and network contacts for insider perspective.

### 4. Location & Logistics (Pass/Fail + Notes)
[Define your own rule here — e.g.:]
- Within commute range of [your city], or remote: PASS
- Requires relocation: [PASS if you're open to it / FAIL if not — per `Application_Answers.md`]
- Frequent international travel: FLAG (discuss with user)

### 5. Career Alignment & Motivation (0-100)
Does this role advance career goals and contain tasks that energize?

| Score | Meaning |
|-------|---------|
| 80-100 | Strongly aligned with career direction, clear growth path |
| 60-79 | Good role but only partially aligned with long-term goals |
| 40-59 | Decent job but doesn't build toward career goals |
| 0-39 | Dead end or backwards step |

**Career goals** *(fill in — this is the single most important input to this dimension)*:
- [What are you actually trying to move toward? Be specific — role type, industry, seniority trajectory.]

**Motivation filter** *(fill in)*: Evaluate not just whether the
candidate *can* do the tasks, but whether they'll *energize* you.
- **Energizes:** [List 2-4 kinds of work that genuinely engage you.]
- **Drains:** [List 1-3 kinds of work you want to avoid.]
- **Non-task factors:** [e.g. leadership style, autonomy, whether the team ships real products vs.
  maintains legacy systems.]

**Life situation** *(from `Application_Answers.md` — not a guess)*:
- [Any timing constraints — e.g. finishing a degree, notice period, relocation timeline.]
- [Sponsorship/visa situation, if it affects how you present availability.]
- [Relocation openness.]
- [Salary policy, if you have one you want factored in.]

## Output Format

Present the evaluation as:

```
## Job Fit Evaluation: [Role] at [Company]

| Dimension | Score | Notes |
|-----------|-------|-------|
| Technical Skills | XX/100 | [brief note] |
| Experience Match | XX/100 | [brief note] |
| Behavioral Fit | XX/100 | [brief note] |
| Location | PASS/FAIL | [brief note] |
| Career Alignment | XX/100 | [brief note] |

**Overall Score: XX/100** (weighted average of scored dimensions)

### Verdict: [Strong Fit / Good Fit / Moderate Fit / Weak Fit / Poor Fit]

### Key Strengths for This Role
- [bullet points]

### Gaps to Address
- [bullet points]

### Recommendation
[1-2 sentences: apply/skip/apply with caveats]

### Company Research Checklist
- [ ] Checked company website (mission, values, recent news)
- [ ] Checked review sites (Glassdoor, etc.)
- [ ] Checked LinkedIn for team size, recent hires, connections
- [ ] Checked media for restructuring, growth, or workplace issues
- [ ] Identified network contacts who may know the team/manager
```

Company research is one-off per posting — there's no cache file in this workflow.
Any claim from this research that lands in the final cover letter still needs the
independent verification required by `writing-style.md` rule 5 before it's included.

## Weighting
- Technical Skills: 30%
- Experience Match: 25%
- Behavioral Fit: 15%
- Career Alignment: 30%

(Location is pass/fail, not weighted)

Adjust these percentages if a different weighting better reflects what actually matters to you.

## Thresholds
- **Strong Fit** (75+): Definitely apply, tailor everything
- **Good Fit** (60-74): Apply, address gaps in cover letter
- **Moderate Fit** (45-59): Consider carefully, discuss with user
- **Weak Fit** (30-44): Probably skip unless strategic reasons
- **Poor Fit** (<30): Skip

## Pre-Application: Call the Employer (Best Practice)

Before writing the application, consider whether to call the contact person listed in
the posting. **Only call if there are substantive questions** — never call just to "be
remembered."

### When to Suggest Calling
- The posting has unclear or ambiguous requirements
- It's unclear which competencies are essential vs. nice-to-have
- The role description is vague about day-to-day tasks
- There's a named contact person who invites questions

### Good Questions to Ask
- "What are the primary challenges in this role?"
- "How is time typically divided across the listed responsibilities?"
- "Which competencies are most critical for success in this position?"
- "What does success look like in the first 6-12 months?"

### Rules for the Call
- Prepare a 30-second "elevator pitch" in case they ask
- The call's purpose is **gathering information**, not delivering a pitch
- Take notes — use what's learned to tailor the application
- Reference the conversation naturally in the cover letter ("After speaking with
  [name], I was especially drawn to...")
