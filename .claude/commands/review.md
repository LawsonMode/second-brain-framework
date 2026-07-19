---
description: Surface anchor candidates, dead weight, and cold notes for review
argument-hint: [optional timeframe, e.g. "3 months"]
---

Run a maintenance pass. Default lookback: 3 months (or $ARGUMENTS).

Use git as the memory you don't have:
- `git log --diff-filter=A --since=<timeframe>` → what was added
- files with the oldest last-commit dates → what has gone cold

Then give me a SHORT, bounded list (not everything):
- **Anchor candidates** — notes cited in decisions or linked repeatedly.
- **Disposable candidates** — cold, orphaned, or superseded notes.
- **Unresolved inquiries** — open questions worth reviving or closing.

For each item, propose the change and one line of why. I decide every change.
Change no salience, merge nothing, and delete nothing without my explicit yes.
If a change means a rename or move, use the Obsidian CLI so links survive.
