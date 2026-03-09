---
name: book-study
description: |
  Comprehensive multi-book study that traces intellectual evolution across an author's or tradition's body of work. Analyzes multiple books together, identifies how ideas develop and transform, and optionally suggests reading order based on conceptual dependencies. Produces a unified HTML slide presentation and a markdown study guide. Invoke with /book-study.
argument-hint: "[paths to multiple .epub, .pdf, or book files]"
---

# Book Study Skill

You will create two outputs from **multiple book files**:
1. A comprehensive **markdown study guide** (`[study-name]-study-guide.md`)
2. A unified **HTML slide presentation** (`[study-name]-study.html`)

The presentation traces how ideas develop, transform, and interact across a body of work — not just summarizing each book individually.

Follow the seven phases below. Phases 5a and 5b are independent and can run in parallel.

---

## Phase 1: Extract & Read All Books

### For each book file, detect type and extract content in parallel:

**For `.epub` files:**
1. Create a unique temp directory per book: `mktemp -d /tmp/book-extract-XXXXXX` then `unzip book.epub -d $TMPDIR`
2. Read OPF/NCX to identify chapter order
3. Launch **3-5 parallel Explore agents per book**, each covering a chapter range
4. Each agent extracts: key arguments, quotable passages, chapter themes, striking metaphors

**For `.pdf` files:**
- Read with page ranges, launch parallel agents per page range

**For plain text / `.txt` files:**
- Split into logical sections for parallel processing

### Critical: Launch extraction for ALL books simultaneously. If you have 3 books, you should have 9-15 agents running at once. This is the key performance optimization.

---

## Phase 2: Individual Analysis

For each book, synthesize its agents' findings into:
1. **Core thesis** — the book's central argument in 2-3 sentences
2. **Structural outline** — how the argument builds
3. **15-25 best excerpts** per book (fewer per book than single-book mode, since space is shared)
4. **Key concepts introduced** — what new vocabulary, frameworks, or ideas does this book contribute?
5. **Publication context** — when was it written, what was the author responding to?

---

## Phase 3: Cross-Book Analysis & Reading Order

This is the phase that distinguishes a study from a collection of book reports.

### 3a. Identify Cross-Book Threads

Find **conceptual threads** that run across multiple books:
- **Evolving concepts**: Ideas that the author refines, revises, or abandons across works (e.g., Kuhn's "incommensurability" shifting from perceptual to linguistic)
- **Recurring tensions**: Contradictions or unresolved questions the author keeps returning to
- **Building blocks**: Concepts from earlier works that later works presuppose or extend
- **Reversals**: Places where the author explicitly changes position
- **Vocabulary shifts**: When the same word means different things in different works, or when new terminology replaces old

For each thread, note:
- Which books participate
- How the idea transforms at each stage
- The most revealing excerpt from each book showing the transformation

### 3b. Determine Reading Order

Analyze the corpus and determine **two orderings**:

1. **Chronological order**: By publication date — the order the author actually wrote them
2. **Recommended study order**: Based on conceptual dependencies. Consider:
   - Which books introduce foundational concepts others build on?
   - Which books are more accessible entry points?
   - Are there works that only make sense after reading earlier ones?
   - Does reading order affect how you interpret the argument?

If chronological and recommended orders differ, explain why. If the user has specified a preferred order, respect it.

### 3c. Plan the Narrative Arc

Design the presentation's flow. The presentation should NOT be "Book 1 slides, then Book 2 slides, then Book 3 slides." Instead, organize by **conceptual progression**:

- Start with the foundational ideas (whichever book introduces them)
- Follow each thread as it develops across books
- Use **cross-reference slides** at key moments to show evolution
- Use **book transition slides** to orient the reader when shifting focus
- Build toward the most mature or provocative formulation of the core ideas

---

## Phase 4: Write Margin Annotations

For each selected excerpt, write **2-3 margin notes**. Follow the same quality standards as the book-club skill, with one addition:

### Cross-book annotations are the unique value-add:
- **Forward references**: "This definition will be significantly narrowed in [Later Book], where..."
- **Backward references**: "Compare the more tentative formulation in [Earlier Book]: '...'"
- **Evolution markers**: "Notice how [concept] has shifted from [meaning A] to [meaning B] since [Book]"
- **Tension surfacing**: "This claim sits uneasily with [Author]'s own argument in [Other Book] that..."

### Labels must be:
- Descriptive concepts: "Semantic Drift", "The Revised Criterion", "Abandoned Framework", "Conceptual Continuity"
- Bad: "Connection!", "Cross-Reference", "See Also", "Compare"

### Note body rules (same as book-club):
- **Analytical, not summary** — NEVER restate what the excerpt says
- **Cross-referential** — connect across books, to other thinkers, to broader traditions
- **Hidden implications** — surface what the reader might miss
- **Concrete** — use specific examples, named thinkers, real events

---

## Phase 5a: Generate Markdown Study Guide

Create a comprehensive markdown document with:

1. **Title and metadata** — study title, author(s), books covered with publication years
2. **Opening** — a signature passage that captures the intellectual project's essence
3. **Study overview** — 3-5 paragraphs on the author's intellectual journey: why these books matter together, what the arc reveals that individual books cannot
4. **Reading order recommendation** — chronological listing AND recommended study order with rationale for each position
5. **The intellectual arc** — how the central ideas develop across the corpus, told as a coherent narrative with key quotations from each book
6. **Conceptual threads** (4-8 sections) — each thread gets:
   - Explanatory prose tracing the idea across books
   - 2-4 excerpts from different books showing the evolution
   - Analysis of how and why the concept changed
   - Connections to broader intellectual traditions
7. **Individual book summaries** — for each book (in recommended reading order):
   - Core thesis (2-3 paragraphs)
   - Unique contributions (what this book adds that others don't)
   - 3-5 key quotations
   - Position in the larger project
8. **Critical perspectives** — major critiques of the author's project, especially those that engage with the evolution across works
9. **Unresolved tensions** — questions the author never fully settled
10. **Discussion questions** — 8-12 questions, at least half requiring knowledge of multiple books
11. **Key quotations collection** — 20-30 passages organized by theme, drawn from across all books

Save as `[study-name]-study-guide.md`. Derive the name from the author or unifying theme: e.g., `kuhn-incommensurability-study-guide.md`.

---

## Phase 5b: Generate HTML Slides

1. **Read the template** from [assets/study-template.html](assets/study-template.html)
2. **Read the design guide** from [references/design-guide.md](references/design-guide.md)
3. **Replace placeholders**:
   - `{{STUDY_TITLE}}` → the study's title (e.g., "The Evolution of Incommensurability")
   - `{{SIDEBAR_SUBTITLE}}` → "Author Name" or "Author Name & Author Name"
   - `{{BOOKS_SUBTITLE}}` → number of books (e.g., "A Study in Three Books")
4. **Populate slides** inside `<div class="slides-wrapper">`:

### Slide structure:

- **Slide 0 — Title**: `class="slide active no-margin"` — study title, author, book count, a unifying quotation. Uses `study-title-page` class. Includes `begin-hint`.

- **Slide 1 — Library**: `class="slide no-margin"` — overview of all books in the study. Uses `.book-card` elements showing each book's title, year, and one-line thesis. Books listed in recommended reading order.

- **Slide 2 — Roadmap**: `class="slide no-margin"` — the intellectual arc in brief. Uses a `.timeline` or `.evolution-diagram` showing how the central idea develops. Frame what follows.

- **Slides 3 through N — Content slides** (the bulk): A mix of:
  - **Excerpt slides** (`class="slide"`): Same as book-club — direct excerpts with margin notes. The `page-chapter` label includes the book title: `"Book Title &middot; Chapter N"`.
  - **Evolution slides** (`class="slide evolution-slide"`): Side-by-side or sequential comparison of how a concept appears in different books. Uses `.evolution-panel` elements.
  - **Book transition slides** (`class="slide no-margin book-transition"`): Brief orienting slide when focus shifts to a new book. Shows book title, year, and a one-sentence framing of what this book contributes.
  - **Thread slides** (`class="slide no-margin"`): Synthesis slides that step back and analyze a cross-book pattern. Uses commentary prose, not excerpts.

- **Slide N+1 — Reading Order**: `class="slide no-margin"` — recommended reading order with rationale. Uses `.reading-order-item` elements.

- **Slide N+2 — Discussion**: `class="slide no-margin"` — 6-8 thought-provoking questions, prioritizing cross-book questions.

- **Slide N+3 — Closing**: `class="slide no-margin"` — the intellectual project distilled + a final quotation + attribution.

### Formatting rules:
- Same typographic rules as book-club (elisions, em-dashes, smart quotes, drop caps)
- Each slide needs a descriptive `data-title` attribute
- First slide has `class="active"`
- Use `data-book` attribute on excerpt slides to identify which book (enables subtle visual differentiation)
- `page-chapter` labels on excerpt slides MUST include the book title for orientation

### Slide count guidance:
- **2-3 books**: 30-45 total slides
- **4-5 books**: 40-55 total slides
- **6+ books**: 50-65 total slides
- Roughly 40% excerpt slides, 25% evolution/cross-reference slides, 15% thread/synthesis slides, 20% structural slides (title, library, transitions, discussion, closing)

Save as `[study-name]-study.html`. Use the same naming convention as the study guide.

---

## Phase 6: Determine Conceptual Weight

Not all books in a study deserve equal representation. Allocate slide count based on:

1. **Conceptual density** — books that introduce more foundational ideas get more slides
2. **Pivotal moments** — books where the author makes major revisions deserve emphasis
3. **Accessibility** — the most approachable book might deserve slightly more space as the entry point
4. **Uniqueness** — if two books cover similar ground, favor the more developed treatment

A minor or transitional work might get 3-4 excerpt slides; a magnum opus might get 8-12.

---

## Phase 7: Refine

Review both outputs:

1. **Arc check**: Does the presentation tell a coherent story of intellectual development? Can a reader unfamiliar with any of the books follow the progression?
2. **Cross-reference audit**: Are there enough evolution slides and cross-book margin notes? The presentation should feel like a *study*, not a playlist of book summaries.
3. **Balance check**: Is any book over- or under-represented relative to its importance?
4. **Margin note audit**: Verify no margin note merely restates its excerpt. At least 30% of margin notes should make cross-book connections.
5. **Flow check**: Do book transitions feel natural? Is the reader oriented about which book they're reading from at all times?
6. **Reading order clarity**: Is the recommended reading order clearly justified?
7. **Consistency check**: Both the study guide and slides should reference the same threads and key excerpts
8. **Technical check**: Well-formed HTML, all slides have `data-title`, first slide has `class="active"`

---

## Important Notes

- **This is a study, not a collection**: The value is in tracing connections and evolution. If you removed the cross-book analysis, you should lose at least 30% of the content.
- **Direct excerpts only**: Show the author's actual words. Let the margin notes and synthesis slides provide the analysis.
- **Respect the author's development**: Don't flatten evolution into consistency. If the author changed their mind, show that. If they contradicted themselves, surface it.
- **The margin notes are the value-add**: Cross-book margin annotations — showing how an idea from page 47 of Book A connects to page 203 of Book C — are what make this a *study* rather than a bibliography.
- **Single-file HTML**: Completely self-contained. All CSS/JS inline. Only external dependency is Google Fonts CDN.
- **Reading order is optional but valuable**: Always provide it. Let the user decide whether to follow it.
