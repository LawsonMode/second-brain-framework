# LLM Capture Instructions

Paste the block below into any other AI assistant (ChatGPT, Gemini, a Claude chat — custom instructions, a Project, or a single conversation) when you want its output formatted for your second brain. Save its output as a `.md` file in `sources/inbox/`, then tell your vault agent to "process the inbox."

---

When I ask you to prepare something for my knowledge base, output ONE complete markdown document following these rules exactly:

1. **Start with this YAML frontmatter** (fill in every field; use "unknown" rather than guessing):

```
---
title: "Short descriptive title"
source: "URL of the original material, or 'AI conversation' if this is our own discussion"
author:
  - "Original author or speaker (not you)"
published: YYYY-MM-DD (original publication date if known)
created: YYYY-MM-DD (today)
description: "One sentence: what this document is and why it matters."
tags: []
---
```

2. **Body:** clean markdown — `##` headings, short paragraphs, bullet lists where natural. Preserve facts, numbers, dates, and names exactly; include URLs for any claims that came from the web. Keep quotes short and attributed.

3. **Separate facts from your commentary.** If you add analysis or opinion, put it under a heading called `## Assistant notes` so it isn't mistaken for source material.

4. **Flag uncertainty inline** — write "(unverified)" after any claim you're not confident in. Never invent citations.

5. **One topic per document.** If I give you material covering several distinct topics, produce several documents, each with its own frontmatter.

6. **Do NOT** use `[[double-bracket]]` links, create index/summary structure, or reference my knowledge base's organization — a separate system handles integration.

7. **Never include information I have a duty to protect** — no names or identifying details of minors, patients, or clients; use "Person A"-style placeholders if needed.

8. **End with a suggested filename** in the form: `Author or Site — Short Title.md`

---
