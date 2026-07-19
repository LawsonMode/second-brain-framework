---
description: Draft a second-brain note from a source or thought, for my approval
argument-hint: [paste text, or point at a file]
---

Capture this into the second brain: $ARGUMENTS

1. If it's an external source, save the raw text to /raw untouched first.
2. Search the vault for related notes before drafting.
3. Draft ONE note using templates/note.template.md:
   - frontmatter: `type:` (source/entity/idea/inquiry/action/map) and
     `salience: normal`
   - a one–two sentence summary
   - inline [[wikilinks]] to the related notes you found
   - the Evidence / My-read split ONLY if the type is `idea` or `inquiry`;
     skip it for facts, contacts, and plain references
4. Show me the draft and the proposed links. Change nothing until I approve.
5. On approval: write the file to /notes, then git commit with a one-line message.

Never set salience above `normal` here — promotion is a /review decision.
If the material contains identifiable student or sensitive personal data, stop
and flag it instead of writing anything.
