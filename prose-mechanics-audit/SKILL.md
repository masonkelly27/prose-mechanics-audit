---
name: prose-mechanics-audit
description: "Use only when the user explicitly asks for a prose audit or names a specific audit: 'audit prose', 'run the [name] audit', 'active/passive audit', 'sentence variance', 'parallel structure check', 'readability audit', 'prose mechanics'. Flags and explains sentence-level issues; never edits the manuscript or suggests rewrites. For general critique or line editing, use story-review instead."
---

# Prose Mechanics Audit

Diagnostic audits for sentence-level prose quality. Each audit is a focused pass that produces a flagged-issues report explaining what was found and why it matters. The author decides what, if anything, to change, and makes every change themselves. Works for fiction or nonfiction.

Adapted from `prose-mechanics` in rhavekost/author-toolkit (MIT license; see `LICENSE`). This version removes all manuscript editing and all suggested fixes.

## The Two Hard Rules

These override everything else in this skill and every reference file:

1. **Never alter the manuscript.** Do not edit, rewrite, overwrite, rename, move, or delete any manuscript file or chapter, in whole or in part, by any means. This holds even when the author asks during an audit; an audit's output is a report, never a changed manuscript.
2. **Never suggest replacement wording.** Do not offer rewritten sentences, alternative phrasings, synonym options, "consider X instead," or before/after versions of the author's prose. Explain what the issue is and why it costs the reader; leave the solution to the author.

Explaining the *nature* of an issue is required and is not a suggestion: "the actor of this sentence is buried in a passive construction," "'stone' repeats nine words after its first use," "the list shifts from gerunds to an infinitive." Naming how to fix it is not.

## Files This Skill May Create

Reports, notes, and trackers are allowed. They are written as **new files only**, never into a manuscript file:

- `audit-tracker.md` in the project folder (copied from `assets/audit-tracker-template.md` if it doesn't exist)
- audit reports in `reports/prose/<chapter>--<audit>--<date>.md`
- session notes in `sessions/`

If the author is working in chat with pasted text rather than in a project folder, deliver the report in the conversation and skip the files.

## Session Continuity

Audit work is iterative across multiple sessions. Claude has no memory between them, so the audit tracker is your persistent state.

- **At session start:** Read `audit-tracker.md` in the project directory if it exists. Check which audits have run on which chapters and what's still outstanding.
- **At session end:** Update the tracker with what was audited and what was flagged. Note the stopping point.
- **Surface unresolved flags:** If prior audits flagged issues the author hasn't marked as addressed, list them at session start so the author can decide what to take on.

## Core Concept

Audits are diagnostics, not edits. Each pass scans for one specific class of issue, produces a list of flagged passages with explanations, and stops. The author decides whether each flag is a real problem or a deliberate choice, and how to handle it.

## When to Use

This skill is for:
- ✅ Sentence-level audits on finished or near-finished drafts (fiction or nonfiction)
- ✅ Final polish before submission, querying, or publication
- ✅ Catching the mechanical issues that survive developmental editing
- ✅ Short passages, when the author explicitly asks for an audit. Note in the report that count-based audits (frequency, sentence variance, readability) are unreliable on small samples.

## When NOT to Use

This skill is NOT for:
- ❌ General critique, line editing, or editorial review — use `story-review`
- ❌ Macro structure — use `story-structure`
- ❌ Early drafting or prose generation
- ❌ Manuscripts still being restructured (audited prose may be cut)
- ❌ Heavy stylistic departures where an audit's assumptions don't hold — if you run one anyway, say which assumptions don't apply

## Style-Sensitive Audits

Some audits encode commercial-fiction conventions rather than errors: Readability, Sentence Variance, Filter Words, Adverbs, Dialogue Tags, Sticky Sentences, Sentence Starters, Clichés, and Show vs. Tell. In literary prose, deliberate long or nested sentences, filtered perception, and summarized emotion are often choices, not faults. When running these, explicitly consider whether a flagged pattern is a voice choice, and say so in the report when it plausibly is.

## Audit Passes

Run audits **one at a time**. Recommended sequence: frequency-family first, mechanical passes next, semantic passes last (judgment-expensive; don't run on prose about to be reworked). If the author requests a different order, follow it.

| # | Audit | Class | Invocation | Catches |
|---|-------|-------|------------|---------|
| 1 | Active/Passive | hybrid | "Run active/passive audit on..." | Unjustified passive, hidden agency |
| 2 | Parallel Structure | semantic | "Run parallel-structure audit on..." | Broken grammatical parallels |
| 3 | Sentence Variance (file: `sentence-length-variance.md`) | deterministic | "Run sentence-variance audit on..." | Flat rhythm, narrow length bands |
| 4 | Readability (file: `accessibility-audit.md`) | deterministic | "Run readability audit on..." | Grade-level spikes, paragraph bloat |
| 5 | Echoes | deterministic | "Run echoes audit on..." | Word repeated within 100 words |
| 6 | Frequency | deterministic | "Run frequency audit on..." | Chapter-wide word overuse |
| 7 | Crutch Words | deterministic | "Run crutch-words audit on..." | Author-specific overused words |
| 8 | Filter Words | deterministic | "Run filter-words audit on..." | felt/saw/heard/realized/noticed/watched |
| 9 | Adverb Audit | deterministic | "Run adverb audit on..." | -ly density, dialogue vs. narration |
| 10 | Dialogue Tags | hybrid | "Run dialogue-tags audit on..." | Said-bookisms, adverb-modified tags |
| 11 | Sticky Sentences | deterministic | "Run sticky-sentences audit on..." | Glue-word density |
| 12 | Sentence Starters | deterministic | "Run sentence-starters audit on..." | Repeated opener patterns |
| 13 | Tense Consistency | hybrid | "Run tense-consistency audit on..." | Unintentional tense flips |
| 14 | Invented-Term Consistency | deterministic | "Run invented-term-consistency audit on..." | Capitalization drift in invented names |
| 15 | Clichés | hybrid | "Run cliches audit on..." | Well-worn phrases |
| 16 | Pronoun Clarity | semantic | "Run pronoun-clarity audit on..." | Ambiguous antecedents |
| 17 | Show vs. Tell | semantic | "Run show-vs-tell audit on..." | Named vs. dramatized emotion |
| 18 | POV Consistency | semantic | "Run pov-consistency audit on..." | Head-hopping, knowledge violations |

Load only the reference file matching the currently invoked audit. Do not preload all references. If switching audits mid-session, load the new reference file and treat the prior one as out of scope.

All audits are performed by reading the text and applying the reference file's detection rules directly. Do not run external programs against the manuscript.

## Finding Format

Every finding follows `references/finding-schema.json`:
`audit`, `technique`, `severity` (note/suggestion/warning), `location`
(file/line/quote), `issue`, `confidence` (deterministic/judgment).
Render findings grouped by severity. The severity label "suggestion" means
"worth a look," not a proposed rewrite.

## Workflow

For each audit:

1. **Scope:** Confirm which chapter(s) or passage(s) to audit. Audit one chapter at a time unless the author asks for broader scope.

2. **Run the pass:** Read the prose looking for the specific patterns named in the relevant reference file. Do **not** look for other classes of issue — keep the lens narrow.

3. **Produce a flagged-issues report.** For each flag:
   - Location (file and approximate line, or paragraph for pasted text)
   - The flagged text (short excerpt)
   - Which detection pattern matched
   - Why it may cost the reader, and whether it could plausibly be a deliberate choice

   Group recurring instances as a pattern with representative examples rather than listing every hit when there are many.

4. **Stop. Hand the report to the author.** The author decides which flags are real and handles them personally.

5. **Update the tracker** (if working in a project folder): which audit ran, on which chapter, how many flags, and where the report lives.

6. **Move to the next audit only when the author asks.**

## Common Mistakes

| Mistake | Why It Happens | Fix |
|---------|---------------|-----|
| **Offering a rewrite** | Habit of being helpful | Explain the issue; stop there. The author fixes. |
| **Running all audits simultaneously** | Wanting to be thorough in one pass | Each audit has a different lens. Stacked, they produce a noise-flood. One pass at a time. |
| **Treating flags as verdicts** | Mechanical pattern-matching | A flagged passive may be the right passive. Say when a flag could be a choice. |
| **Auditing unstable drafts** | "Polish as I go" instinct | If chapters are still being cut or reordered, note it and confirm before auditing. |
| **Drifting outside the audit's lens** | Noticing other issues | Ignore issues outside the current audit's scope. Mention, at most, that another audit might be worth running. |

## Self-Check: Is This Working?

**Before starting an audit:**
- [ ] Is the audit scope clearly defined (which chapter, which passages)?

**During an audit:**
- [ ] Am I using only the patterns from the relevant reference file?
- [ ] Am I producing a report, with no edits to any manuscript file?
- [ ] Have I avoided writing any replacement wording?

**After producing the report:**
- [ ] Can the author understand each flag without re-reading the reference?
- [ ] Did each flag include an excerpt, the matched pattern, and the reason it matters?
- [ ] Did I stop and wait rather than continuing to the next audit?
- [ ] Did I update the tracker (project-folder work only)?

If you answered "no" to any checkpoint, resolve it before continuing.

## Stopping Points

Each audit ends when its report is delivered. Do not auto-advance to the next audit, do not silently widen the audit's lens, and never modify the manuscript.

| Phase | Stop when... | Then |
|-------|--------------|------|
| **Any single audit** | Flagged-issues report for the requested scope is delivered | Wait for the author. |
| **Audit sequence** | Author defers, OR a later audit reveals the manuscript needs structural work | Stop. Note in tracker. Recommend `story-review` or `story-structure` for the structural pass. |
| **Session** | Stopping point reached or context window is filling | Update `audit-tracker.md`; write a `sessions/` note; stop. |

## Quick Reference Commands

| Need | Command |
|------|---------|
| Start audit sequence | "Run the prose-mechanics audits on [chapter]" |
| One audit | "Run [audit name] audit on [chapter or passage]" |
| Check audit status | "What audits have run on [chapter]?" |

---

## Files

- `references/*.md` — one detection spec per audit
- `references/finding-schema.json` — finding format
- `assets/audit-tracker-template.md` — per-project tracker for audit runs
- `LICENSE` — original MIT license from rhavekost/author-toolkit
