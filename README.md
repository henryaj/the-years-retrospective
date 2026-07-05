# the-years-retrospective

An agent skill for building multi-year life retrospectives from two triangulated sources: a personal journal (voice, interiority, quotes) and calendar history (ground truth of behavior). Fans out one subagent per calendar year, collects structured briefs, and synthesizes a final document in whatever register the invocation asks for — a toast, a therapist's read, an annual letter.

Where the journal and the calendar disagree, the skill trusts the calendar: journals over-record pain and go quiet in good seasons; calendars record that you kept showing up.

## Install

```bash
npx skills add henryaj/the-years-retrospective --agent claude-code
```

The `--agent claude-code` flag matters: without it the CLI may only place the canonical copy in `~/.agents/skills/`, which Claude Code doesn't read — you want it in `~/.claude/skills/` (add `-g` for global, or run inside a project for project scope).

## Requirements

- A journal corpus on disk (dated markdown files work best)
- Calendar access (e.g. a Google Calendar MCP connector)
- An agent harness with subagent support (built for Claude Code)

## Usage

In Claude Code, invoke it as a slash command:

```
/the-years-retrospective
```

A bare invocation covers the whole journal span in the default register — a fond, sharp, off-duty therapist's toast, with per-year chapters, a cross-year read, and a designed artifact as the deliverable. Add arguments to override any of the defaults:

```
/the-years-retrospective the last five years, as a sports commentator's season recap
/the-years-retrospective 2020–2024, focus on career; keep it to two pages
```

The skill handles the machinery either way: scoping coverage, per-year agent fan-out, brief collection, quote verification against sources, and honest reporting of journal-thin years.
