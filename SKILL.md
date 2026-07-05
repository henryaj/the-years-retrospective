---
name: retrospective
description: Use when the user asks for a multi-year retrospective, life review, "the years," a year(s)-in-review document, an annual letter, or any synthesis spanning long stretches of a personal journal/diary and calendar history.
---

# Multi-year retrospective — journal × calendar fan-out

Build the document from two sources triangulated: the journal (voice, interiority, quotes) and the calendar (ground truth of behavior). Where narration and behavior diverge, trust behavior — journals are biased instruments that over-record pain and go quiet in good seasons; the calendar records that the person kept showing up. One subagent per calendar year produces a structured brief; synthesis happens in the main context, which holds the user's spec.

The register, structure, and rules of the final document come from the user's invocation prompt. This skill covers the machinery, not the voice.

## Before spawning anything

1. Gather corpus caveats: check memory/project notes for known data traps (OCR dating errors, duplicate imports, stub files, where the real content actually lives, a people glossary). If none exist, build them by inspection — sample files, check frontmatter, count words — and save what you learn for next time. Feed the relevant caveats into every agent prompt.
2. Scope coverage: list journal files grouped by year, with word counts per year. Years with low volume (roughly <5k words; prorate for partial years) are **journal-thin**: their agents must be told "calendar is your primary source; reconstruct behaviorally; don't apologize for the gap." The current year's window ends today.
3. List calendars once; pass explicit calendar IDs to agents. Primary always; when unsure whether a secondary calendar (social imports, work) reaches a given year, pass it anyway — a zero-event result is itself evidence.

## Per-year agents (one per calendar year, parallel, general-purpose)

Each prompt must be self-contained: the people glossary; exact journal file paths for that year; calendar IDs with time window, `orderBy: startTime`, `pageSize: 250`, paginate to exhaustion; the standing caveats; and the brief format — coverage report, dated timeline, recurring commitments (deduped: a weekly ritual is ONE fact), new people/places/projects, candidate highlights, candidate quotes (verbatim + dated, selected for aliveness/craft/foreshadowing, not maximal sadness), emotional weather, neutral pattern notes, small forgotten details. Extend the brief format with register-specific fields the invocation needs (stats, pattern notes, etc.).

Three lines that must appear in every agent prompt:
- "Trust your own calendar/journal evidence over any facts I've primed you with; flag discrepancies explicitly." (Orchestrator priming from stale memory has been wrong before — in one run, a residency was mis-dated by five months.)
- "Your final text is returned to the orchestrator as data, not shown to the user — return only the brief."
- "Read-only: do not modify any source file."

## Collecting briefs — the idle trap

Background agents finish and go **idle without sending anything**; the idle notification carries no content. On each idle notification with no brief received, immediately `SendMessage` that agent: "Send me the completed brief now, as one message addressed to me." Expect to do this for most agents. If an agent still returns nothing after one nudge, respawn that year once; failing that, ship with the hole declared in the footer. Relay sibling findings when agents' windows interlock (who dates a shared voice memo, when a house move actually happened) and ask reconciliation questions explicitly.

## Synthesis (main context, not a subagent)

- Reconcile cross-year conflicts before writing; prefer the agent with more/denser evidence.
- **Verify quotes before publishing**: grep the ~20 most load-bearing quoted phrases against the journal sources. Every quote in the document carries a date.
- Characterological claims need behavioral (calendar) support, not just journal narration; claims resting on a single entry don't ship.
- If the spec makes psychological or arc-shaped claims (growth, comebacks, patterns): growth-frame gate — an arc without demonstrated movement in the record doesn't ship (route it to a companion doc if one exists); ration interpretations to 1–2 per year chapter; absences are questions, never findings.

## Publishing

If a design/artifact skill is available, load it; give the document its own visual identity (don't reuse a prior document's look). Footer must state method and coverage honestly — which years were journal-thin, what was reconstructed, that corrections will be marked visibly, version + date. Assume the user will check citations; weave revisions in visibly, never silently patch.

## Known traps

| Trap | Counter |
|---|---|
| OCR filename year wrong | Weekday cross-check: "Sunday July 6th" in the text pins the real year |
| Duplicate OCR runs of same pages | Read one of each pair (record pairs in the corpus caveats) |
| Stale orchestrator priming | Agents instructed to trust their own evidence and flag conflicts |
| Agent idle, no brief | SendMessage demanding the brief as a message |
| Events while abroad | Render in the calendar's home timezone; dates can shift a day — tell agents to infer abroad-periods from flights |
| Quiet journal stretch read as decline | Often the person was demonstrably active — check calendar density first |
