# Knowledge Base

This directory contains your company documentation that the Q&A pipeline searches. Organise your content into subdirectories by type.

## Directory Structure

```
knowledge-base/
├── products/       # Product documentation, specs, guides
├── faqs/           # Frequently asked questions
├── policies/       # Company policies, terms, conditions
└── README.md       # This file (excluded from search)
```

## Adding Documents

1. **Write in Markdown** — the retriever works best with `.md` files
2. **Use clear headings** — helps passage extraction find relevant sections
3. **One topic per document** — keeps retrieval focused
4. **Include metadata at the top** — title, last updated date, category
5. **Keep language consistent** — match the terminology your customers use

## Document Template

```markdown
# Document Title

**Last updated:** 2026-02-15
**Category:** products | faqs | policies

## Section Heading

Content here. Keep paragraphs focused on a single point for best retrieval results.
```

## Tips for Good Retrieval

- **Be specific** — "The Widget Pro weighs 250g" retrieves better than "it's quite light"
- **Anticipate questions** — phrase content the way customers would ask about it
- **Update regularly** — stale docs produce stale answers
- **Remove duplicates** — conflicting docs confuse the synthesiser
- **Test with real queries** — use `test-prompt.txt` to verify retrieval quality
