---
name: retrospective
description: Use when the user asks for a multi-year retrospective, life review, "the years," a year(s)-in-review document, an annual letter, or any synthesis spanning long stretches of a personal journal/diary and calendar history.
---

# Multi-year retrospective — journal × calendar fan-out

Build the document from two sources triangulated: the journal (voice, interiority, quotes) and the calendar (ground truth of behavior). Where narration and behavior diverge, trust behavior — journals are biased instruments that over-record pain and go quiet in good seasons; the calendar records that the person kept showing up. One subagent per calendar year produces a structured brief; synthesis happens in the main context.

Everything in "The document" below is the **default spec**. Anything the user's invocation specifies (register, structure, span, rules) overrides the matching default; the defaults fill in everything they don't.

## Part 1 — The machinery

### Before spawning anything

1. Gather corpus caveats: check memory/project notes for known data traps (OCR dating errors, duplicate imports, stub files, where the real content actually lives, a people glossary). If none exist, build them by inspection — sample files, check frontmatter, count words — and save what you learn for next time (to the auto-memory directory or project notes, never into the corpus itself). Feed the relevant caveats into every agent prompt.
2. Scope coverage: list journal files grouped by year, with word counts per year. Years with low volume (roughly <5k words; prorate for partial years) are **journal-thin**: their agents must be told "calendar is your primary source; reconstruct behaviorally; don't apologize for the gap." The current year's window ends today. Map relative spans ("last five years") to whole calendar years: start at 1 January of the earliest year the span touches, and state the chosen window in the overture or footer.
3. List calendars once; pass explicit calendar IDs to agents. Primary always; when unsure whether a secondary calendar (social imports, work) reaches a given year, pass it anyway — a zero-event result is itself evidence.

### Per-year agents (one per calendar year, parallel, general-purpose)

Each prompt must be self-contained: the people glossary; exact journal file paths for that year; calendar IDs with time window, `orderBy: startTime`, `pageSize: 250`, paginate to exhaustion; the standing caveats; and the brief format — coverage report, dated timeline, recurring commitments (deduped: a weekly ritual is ONE fact), new people/places/projects, 3–5 candidate highlights, 5–8 candidate quotes (verbatim + dated, selected per the quote criteria below), emotional weather, **pattern notes** (recurring conflicts, defenses, relational scripts, self-talk habits — logged NEUTRALLY with dates, no interpretation; the cross-year read happens at synthesis), small forgotten details. Extend the brief format with register-specific fields the invocation needs.

Calendar handling rules for agents: signal lives in anomalies (one-offs, travel, dense clusters, names that appear once then keep appearing, firsts and quiet lasts); infer gently, never fabricate — flight + located events = trip, nothing more.

Three lines that must appear in every agent prompt:
- "Trust your own calendar/journal evidence over any facts I've primed you with; flag discrepancies explicitly." (Orchestrator priming from stale memory has been wrong before — in one run, a residency was mis-dated by five months.)
- "Your final text is returned to the orchestrator as data, not shown to the user — return only the brief."
- "Read-only: do not modify any source file."

### Collecting briefs — the idle trap

Background agents finish and go **idle without sending anything**; the idle notification carries no content. On each idle notification with no brief received, immediately `SendMessage` that agent: "Send me the completed brief now, as one message addressed to me." Expect to do this for most agents. If an agent still returns nothing after one nudge, respawn that year once; failing that, ship with the hole declared in the footer. Relay sibling findings when agents' windows interlock (who dates a shared voice memo, when a house move actually happened) and ask reconciliation questions explicitly.

### Synthesis integrity (main context, not a subagent)

- Reconcile cross-year conflicts before writing; prefer the agent with more/denser evidence.
- **Verify quotes before publishing**: grep the ~20 most load-bearing quoted phrases against all quotable sources — journal, daily notes, voice-memo transcripts. Every quote in the document carries a date.
- Characterological claims need behavioral (calendar) support, not just journal narration; claims resting on a single entry don't ship.

## Part 2 — The document (default spec)

### Register

A perceptive therapist who has read everything, genuinely likes the subject, and is slightly off-duty — warm enough to toast, sharp enough that the warmth means something. The true thing said over a drink by someone rooting for them. Not an audit with a party hat on; not a pep talk with "attachment" sprinkled in. First person, addressing the subject as "you."

### Structure

- **Overture**: the whole span in one paragraph; one sentence of the narrator admitting they enjoyed the reading; a note on the instrument (the journal is a rain gauge — it fills in bad weather, so behavior was trusted over narration).
- **Per-year chapters**, each containing: an evocative, earned title (slightly funny is fine); a narrative with momentum — what the year was *about*, not just what happened; a **"Cool stuff you did"** list — concrete, dated, generous, and especially the things they'd wave off (this is the one place a list belongs); 3–6 quotes woven into the prose, never dumped; a **"What your therapist noticed"** aside (see rules below); one small overlooked detail they've certainly forgotten (a menu, a calendar oddity, a pair of socks).
- **Cross-year long read**: the payoff section — spirals tracked across their full arc with dated evidence at both ends; people who arrived and stayed; capacities visibly compounding; unconscious continuities (the thing said in year one and quietly built by year four; the city auditioned for years before the move). Paired quotes years apart on the same theme, set side by side as duets, are worth ten paragraphs of interpretation.
- **By the numbers**: short stat block, only numbers actually countable from the sources.
- **Closing**: one page, written directly to the subject — part toast, part interpretation, all earned. Frame-breaking most welcome here.

### Psychodynamic rules

- **Spiral, not loop.** When a conflict or script recurs across years, narrate its *trajectory*: same theme, shorter recovery, gentler self-talk, bolder response. The signature move: "in [year] this took you four months and 38,000 words; in [year+2] it took five weeks and one entry" — dated at both ends.
- **Growth-frame gate.** A pattern is only named if the record shows movement on it. Raw, unresolved material does not belong in this document — route it to a companion document if one exists, otherwise cut it (don't create a companion unprompted). If unsure which document a finding belongs in, it belongs in the other one.
- **Ration interpretations**: one, at most two, per year chapter. More and the toast becomes a case presentation.
- **Defenses read generously**: humor, busyness, analysis, self-mockery get named the way a fond therapist would — as things that *worked*, that got them through, and that they visibly needed less of over time (only if the record supports that). A defense honorably retired deserves a send-off, not a diagnosis.
- **Frame-breaks**: two or three in the whole document, at the moments of highest earned emotion — "I'm not really supposed to say this, but I was rooting for you here." Budget them; announce in the footer that they were all spent.
- **Hard limits**: no diagnoses; no clinical labels the subject hasn't used themselves; no interpretation resting on a single entry; no wound opened that the document doesn't close (a dark low may be referenced with dignity only when the same document contains its recovery). Speculative reads marked as such: "a hypothesis, held loosely, offered fondly."

### Quote selection

Poignant, not merely sad. Select for: aliveness (wit, wonder, delight recorded live); sentences that are simply well written; hard-won observations; **unknowing foreshadowing** — the subject on the verge of something good without realizing (these hit hardest); small vivid moments rendered specifically. Melancholy only when the arc resolves it. Every quote dated.

### Tone calibration

- Every warm claim and every interpretation anchored to dated evidence. Specificity is the whole game; generic praise and generic insight are equally worthless.
- Funny is welcome; the subject's own jokes may be lovingly redeployed against them.
- Hard periods honored, not laundered: "you got through it, and look what you did anyway — and look how differently you'd handle it now" is the realest celebration available.
- No growth-journey clichés, no LinkedIn cadence, no therapy-speak as decoration.
- **Final gate before publishing**: if the document reads as a roast, redo it. If it reads as pure confetti, redo it. It should read like being seen, fondly, by someone with taste.

### Design & delivery

The default deliverable is a rendered, published page (an Artifact or equivalent), URL relayed to the user; write to the corpus or elsewhere only if asked. Load the design/artifact skill if available, then give the document a bespoke identity matched to the register — never reuse a prior document's look, and avoid clinical/case-file aesthetics for celebratory registers. What worked for the toast register: an evening, lamplit identity — warm near-black ground with an amber/gold accent (full light theme too, token-based); serif display (Baskerville-class, true italics for chapter titles) over a serif body, with letterspaced sans small-caps for dates and labels; a single reading column (~42rem). Signature components: quote blocks with an oversized hanging quotation mark and a small-caps date tag; two-column **duet grids** for paired quotes years apart; cool-stuff lists with accent markers; tinted asides for the therapist observations; large accent year numerals opening each chapter; a tabular-nums stat grid. Typography carries it; keep motion out.

Footer must state method and coverage honestly — sources and volumes, which years were journal-thin and reconstructed, the standing narration-vs-behavior correction, version + date, and that corrections will be woven in and marked visibly, never silently patched. Assume the subject will check citations.

## Known traps

| Trap | Counter |
|---|---|
| OCR filename year wrong | Weekday cross-check: "Sunday July 6th" in the text pins the real year |
| Duplicate OCR runs of same pages | Read one of each pair (record pairs in the corpus caveats) |
| Stale orchestrator priming | Agents instructed to trust their own evidence and flag conflicts |
| Agent idle, no brief | SendMessage demanding the brief as a message |
| Events while abroad | Render in the calendar's home timezone (read it from `list_calendars`; state it in agent prompts); dates can shift a day — tell agents to infer abroad-periods from flights |
| Quiet journal stretch read as decline | Often the person was demonstrably active — check calendar density first |
| Register drifts clinical or saccharine | Run the final gate: roast → redo; confetti → redo |
