# prose-mechanics-audit

A Claude skill for sentence-level prose audits that **flags and explains issues without ever touching the manuscript or suggesting rewrites**.

It runs eighteen focused audits (active/passive, parallel structure, sentence variance, readability, echoes, word frequency, crutch words, filter words, adverbs, dialogue tags, sticky sentences, sentence starters, tense consistency, invented-term consistency, clichés, pronoun clarity, show vs. tell, and POV consistency), one at a time. Each produces a report: what was flagged, which pattern matched, and why it may cost the reader. The author decides what to change and makes every change personally.

## What changed from the original

Adapted from `prose-mechanics` in [rhavekost/author-toolkit](https://github.com/rhavekost/author-toolkit) (MIT license). This version:

- removes every step that edits manuscript files, including fixes the author approves
- removes all suggested fixes, remediation sections, and before/after rewrite examples
- removes calls to the external `scriptorium` command-line tool; every audit is done by reading
- removes the AI-isms audit, which depended on a separate skill
- keeps audit reports, session notes, and the audit tracker (written only as new files)
- narrows the trigger so it loads only when an audit is explicitly requested, leaving general critique to `story-review`
- flags nine audits as style-sensitive, so deliberate literary choices are identified as possible choices rather than errors

## Install (Claude.ai)

Download `prose-mechanics-audit.skill`, then upload it under **Customize → Skills → "+" → Upload skill**.

## License

MIT. The original copyright notice is preserved in `LICENSE` and `prose-mechanics-audit/LICENSE`.
