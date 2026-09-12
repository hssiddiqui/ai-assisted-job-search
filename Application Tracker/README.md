# Application Tracker

One markdown file per job source/board (e.g. `LinkedIn_Applications.md`,
`CompanyCareerPages_Applications.md`, `ClimateJobBoard_Applications.md`) — create a new
one the first time you work a new source. Each file is split into two sections:

```markdown
# Applications Submitted - <source URL, if there is one>

## Applied
- <Role> — <Company> — <Location> — <YYYY-MM-DD> — Applied (<Portal, e.g. Greenhouse/Workday/Lever>) — <link>

## Skipped
- <Role> — <Company> — <Location> — <YYYY-MM-DD> — Skipped — <one-line reason>
```

Keep it a log, not a narrative — one line per posting. This is what `CLAUDE.md`'s SOP
step 1 (duplicate check) searches before opening any new application, and what the
`job-applier` agent updates immediately after every posting (never batched to the end).

Delete this README's example-only nature once you have real tracker files — it's just
here to document the convention for a fresh repo.
