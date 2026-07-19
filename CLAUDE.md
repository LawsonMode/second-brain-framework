# Second Brain — Wiki Schema (v1.0.0)

This vault is an **LLM-maintained wiki**, built on Andrej Karpathy's LLM Wiki pattern
(https://gist.github.com/karpathy/442a6bf555914893e9891c11519de94f).

The core idea: instead of re-reading raw documents on every question (RAG-style),
the LLM incrementally builds and maintains a **persistent, compounding wiki** —
synthesis, cross-references, and contradiction-flagging happen **once, at ingest**,
then stay current. The human curates sources and asks questions; the LLM does the
tedious bookkeeping that makes human-maintained wikis stagnate.

## Three layers

| Layer | Location | Who touches it |
|---|---|---|
| **Raw sources** | `sources/` | Human adds; LLM **reads only — never edits, never deletes** |
| **The wiki** | `wiki/` | LLM creates and maintains; human reads and directs |
| **The schema** | this file | Human approves changes; LLM proposes them |

Support files: `Nexus.md` (home page and content catalog — every wiki page is reachable from it),
`log.md` (reverse-chronological record of every change the LLM makes), and
`Verification Queue.md` (open questions to answer from current records, not guessed —
fed by the `## Needs verification` sections on wiki pages; when the human answers an
item, update the linked pages and check it off).

## Folder map

```
vault/
├── CLAUDE.md              ← this schema
├── Nexus.md               ← home page / catalog (the index)
├── log.md                 ← changelog
├── Verification Queue.md  ← open questions awaiting real-world answers
├── sources/               ← immutable raw material
│   └── inbox/             ← drop zone for new, not-yet-ingested sources
├── wiki/
│   ├── topics/            ← hub pages (Obsidian "MOCs") that map an area
│   ├── concepts/          ← one idea, technique, or pattern per page
│   ├── entities/          ← orgs, tools, projects, places, programs
│   ├── people/            ← one page per human — the CRM layer
│   └── summaries/         ← one page per raw source, distilling it
└── _templates/            ← page templates for each page type
```

## Page types

| Type | Folder | Naming | Purpose |
|---|---|---|---|
| `topic` | `wiki/topics/` | Broad noun phrase, Title Case | Entry-point hub; links out to related concepts/entities/summaries |
| `concept` | `wiki/concepts/` | Singular noun phrase, Title Case | Explains one idea; synthesized across sources |
| `entity` | `wiki/entities/` | Proper name | Facts about an org/tool/project/program, with links to where they appear |
| `person` | `wiki/people/` | Full name | One page per human: who they are, how you know them, interactions, contact context. Grows CRM-style — when the human mentions meeting or talking with someone, update (or create) their page with the date and substance. AI personas stay entities. See **Privacy** below. |
| `summary` | `wiki/summaries/` | `<Author or Site> — <Short Title>` | Faithful distillation of ONE source; cites it in frontmatter |

**Filename = page title.** Use Title Case, no dates in filenames, cross-platform-safe
characters only (no `: / \ * ? " < > |`).

## Frontmatter (required on every wiki page)

```yaml
---
type: topic | concept | entity | person | summary
created: YYYY-MM-DD
updated: YYYY-MM-DD
status: stub | developing | evergreen
sources: []        # file paths under sources/, or URLs
aliases: []        # alternate names for Obsidian link resolution
---
```

## Linking rules

- Use Obsidian wikilinks: `[[Page Name]]`. Link liberally — links are the product.
- Every wiki page must be linked from `Nexus.md` (directly or via a topic hub).
- Summaries link **up** to the concepts/entities they informed; concepts link
  **down** to the summaries that support their claims.
- A claim that matters gets a citation: link the summary page, which cites the raw source.
- If two sources disagree, record both views in the concept page under a
  `## Contradictions` heading — never silently pick a winner.

## Operations

### Ingest (new material arrived)
1. Read each file in `sources/inbox/`. Never modify it.
2. Create a `summary` page in `wiki/summaries/` distilling it.
3. Update or create the `concept`/`entity` pages the source touches; integrate,
   don't append — rewrite sections so the page stays coherent.
4. Move the raw file from `sources/inbox/` to `sources/` (this move is the one
   permitted file operation on sources).
5. Update `Nexus.md`; append an entry to `log.md`.

### Query (human asks a question)
1. Search the **wiki first** (index → topics → concepts), not raw sources.
2. Synthesize an answer with `[[wikilinks]]` as citations.
3. If the answer required going back to raw sources or produced durable new
   insight, file it back into the wiki (then index + log).
4. If the wiki can't answer, say so and name the gap — don't improvise.

### Lint (periodic health check)
1. Orphans: wiki pages not reachable from `Nexus.md`.
2. Contradictions: conflicting claims across pages; surface them under
   `## Contradictions` on the relevant page.
3. Stale pages: `status: stub` older than ~30 days; `updated` far behind related pages.
4. Broken links: `[[links]]` to pages that don't exist (either create a stub or fix the link).
5. Inbox backlog: files sitting in `sources/inbox/` un-ingested.
6. Report findings to the human; fix mechanical issues (links, index) directly,
   ask before content-level rewrites.

## Privacy

Adapt this section to your situation, then hold the LLM to it. Sensible defaults:

- **No pages about people whose data you have a duty to protect** — e.g. minors
  (students, if you teach), patients, clients under NDA. Use neutral placeholders
  ("Student A") when a source mentions them, and never copy identifying details
  into the wiki.
- Keep this vault's remote **private**. Never paste secrets, credentials, or
  account numbers into wiki pages.

## Version control

The vault is a git repository with a **private** remote. At the end of every change
session (ingest / organize / lint fixes), commit with a one-line descriptive message
and push. `.obsidian/workspace*.json` and `.trash/` are gitignored.

## Hard rules

- **Never** edit, rewrite, or delete anything in `sources/` (moving inbox → sources after ingest is the sole exception).
- **Every** change session gets a `log.md` entry: date, operation, pages touched, one-line why.
- Schema changes (this file) are proposed to the human, not made unilaterally; bump the version (semver) when they land.
- Don't create empty scaffolding — a page exists only when there's content (a `stub` with 2 lines and a reason is fine; a blank file is not).
