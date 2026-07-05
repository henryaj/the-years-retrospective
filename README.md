# retrospective

An agent skill for building multi-year life retrospectives from two triangulated sources: a personal journal (voice, interiority, quotes) and calendar history (ground truth of behavior). Fans out one subagent per calendar year, collects structured briefs, and synthesizes a final document in whatever register the invocation asks for — a toast, a therapist's read, an annual letter.

Where the journal and the calendar disagree, the skill trusts the calendar: journals over-record pain and go quiet in good seasons; calendars record that you kept showing up.

## Install

```bash
npx skills add henryaj/retrospective-skill
```

## Requirements

- A journal corpus on disk (dated markdown files work best)
- Calendar access (e.g. a Google Calendar MCP connector)
- An agent harness with subagent support (built for Claude Code)

## Usage

Invoke with a prompt that defines the document you want — span, register, structure, rules. The skill handles the machinery: scoping coverage, per-year agent fan-out, brief collection, quote verification, honest reporting of thin years.
