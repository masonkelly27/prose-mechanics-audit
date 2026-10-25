# Accessibility Audit Reference

A diagnostic pass for readability and structural accessibility at the prose level.

## Scoping Note: Prose Accessibility, Not WCAG

This audit covers **prose accessibility**—the cognitive load a reader experiences when working through the manuscript. It is distinct from **WCAG/disability accessibility**, which governs digital publishing concerns (alt text, semantic HTML, screen-reader compatibility, color contrast, etc.).

WCAG-style accessibility is real and important, but it lives downstream of prose work, with publishers, designers, and platforms. It is intentionally **out of scope** for this audit because:

- The author of an in-progress manuscript rarely controls the final delivery medium.
- The diagnostic tools and remediation patterns are completely different.
- Conflating the two leads to manuscript audits that flag things the author can't fix yet.

If your project includes self-publishing where you control the final output (epub, web, PDF), run a separate WCAG audit at the production stage. This audit is about whether the *prose itself* is reachable for the intended reader.

## What This Audit Catches

- **Reading-grade spikes** that exceed the target for the book's audience.
- **Paragraph bloat:** paragraphs that exceed the length tolerance for the prose register.
- **Sentence complexity spikes:** individual sentences with too many subordinate clauses for the surrounding prose.
- **Header gaps and structural impenetrability:** nonfiction chapters that run hundreds of words without a visual anchor.
- **Jargon and unexplained terminology** introduced without scaffolding.
- **Dense reference chains** ("as discussed in the previous section," "as we'll see later") that fragment comprehension.

## What This Audit Does NOT Catch

- WCAG/disability accessibility (see scoping note above).
- Whether prose is *good*—only whether it is *reachable*.
- Tone, voice, or persona issues (use the voice editor in the relevant skill).
- Whether the content is correct.

## Why It Matters

A book's reach is gated by its accessibility. A reader who has to fight the prose at the sentence or paragraph level will give up before encountering the ideas, regardless of how good those ideas are. This is especially acute for:

- **Self-help and prescriptive nonfiction**, whose readers often pick up the book in moments of stress and have low cognitive bandwidth.
- **Commercial fiction**, where reader retention is measured in pages-per-session and a single bloated paragraph can break the spell.
- **Books for non-native English readers,** where complexity costs compound.

Accessibility is not the same as simplicity. Cormac McCarthy is accessible at the sentence level despite being demanding overall, because each individual sentence is reachable. Accessibility is about whether the next sentence is a step the reader can take.

## Readability Scoring

Use **Flesch-Kincaid Grade Level** as the working metric. It is simple, widely supported, and well-understood by editors and publishers.

**Formula** (Flesch-Kincaid Grade Level):

```
0.39 × (words / sentences) + 11.8 × (syllables / words) − 15.59
```

**Heuristic targets:**

| Audience | Target FK grade |
|----------|-----------------|
| Mass-market commercial fiction | 6–8 |
| Literary fiction | 8–11 |
| General-audience self-help | 6–9 |
| Long-form narrative nonfiction | 8–11 |
| Trade-press intellectual nonfiction | 10–13 |
| Academic / specialist | 12+ |

Flag chapters whose mean grade level exceeds the target by 2+ points, or individual paragraphs that spike 3+ points above the chapter mean.

**Alternatives if FK isn't appropriate:**
- **Gunning Fog Index** — similar but weights long words differently.
- **Dale-Chall** — uses a controlled vocabulary list, better for ESL contexts.
- **SMOG** — emphasizes polysyllabic words; useful for health/medical nonfiction.

Pick one and stick with it across the project; do not mix scores in the same audit.

## Structural Accessibility

Readability scores cover sentence and word complexity. They do not cover **structural** accessibility, which often matters more.

### Paragraph Length

Flag any paragraph that:
- Exceeds 300 words (flat limit regardless of register)
- Runs more than three "ideas" without a break (judgment call)

### Header Density (Nonfiction)

In prescriptive or instructional nonfiction, flag any chapter that runs more than **1,000 words without a subhead, list, callout, or visual break**. Readers in low-bandwidth states need anchors.

This rule is much weaker for narrative nonfiction and memoir; flag only if the prose feels structurally impenetrable, not by word count alone.

### Sentence Complexity Spikes

Flag any sentence that:
- Contains four or more subordinate clauses.
- Has a depth-of-nesting greater than three (clauses inside clauses inside clauses).
- Exceeds 40 words and sits inside a paragraph whose mean sentence length is below 20 words. The local spike, not the absolute length, is the trigger.

### Jargon Introduction

Flag any term that:
- Appears for the first time without definition or context.
- Is used three or more times in a chapter without ever being defined.
- Is a field-specific term in a general-audience book.

## Detection Patterns

A passage is flagged if any of the above thresholds are crossed. Generate the flag list, not a "score." Numbers are inputs to judgment, not verdicts.

## Failure Modes

**Over-application** produces:
- Choppy, dumbed-down prose
- Loss of voice and rhythm
- Patronizing tone in books for adult audiences
- A surface that scores well but reads poorly

**Under-application** produces:
- Readers abandoning the book in the first three chapters
- Reviews that complain about "density" without being able to specify why
- Word-of-mouth ceiling: the book doesn't spread because casual readers can't recommend it

The audit is most useful when paired with the **target reader's actual baseline**. A self-help book aimed at exhausted parents needs different thresholds than a trade-press essay collection aimed at academics on weekends. Set the target before running the audit.

## Worked Examples

### Example 1: Reading-Grade Spike (Self-Help)

**Flagged passage** (FK grade 14.2; chapter mean 8.4):

> The implementation of consistent morning routines necessitates the cultivation of behavioral architectures that operate independent of motivational fluctuation, since reliance upon discretionary willpower invariably produces patterns characterized by sporadic engagement punctuated by extended periods of abandonment.

Flag: grade-level spike of nearly 6 points above the chapter mean. One sentence, four subordinate constructions, multiple polysyllabic terms.

### Example 2: Paragraph Bloat (Narrative Nonfiction)

**Flagged passage:** A 310-word paragraph describing a historical incident, no breath, three distinct sub-events stacked into one block.

### Example 3: Jargon Without Scaffolding (Trade-Press Nonfiction)

**Flagged passage:**

> The hedonic treadmill explains why lottery winners and accident victims return to baseline within months. Our affective forecasting is systematically biased, and the impact bias compounds the error.

Flag: "hedonic treadmill," "affective forecasting," "impact bias" — three field-specific terms in two sentences, none defined.

## How to Run

Perform this audit by reading the text directly. Apply the detection patterns above by eye.
