# Knowledge Base

This directory contains templates, reference guides, and existing documentation that the pipeline agents use.

## Structure

```
knowledge-base/
├── templates/              # Document templates
│   ├── prd-template.md           # Full PRD template
│   ├── feature-brief-template.md # Lightweight feature brief
│   └── technical-spec-template.md # Technical specification
├── reference/              # Reference guides
│   ├── acceptance-criteria-guide.md  # How to write Given/When/Then criteria
│   └── nfr-checklist.md             # Non-functional requirements checklist
└── README.md               # This file
```

## Customisation

Add your organisation's content to make the pipeline more effective:

- **Existing PRDs** — drop previous PRDs into a `existing-prds/` subdirectory
- **API documentation** — add API docs to an `api-docs/` subdirectory
- **Design system** — add component references to a `design-system/` subdirectory
- **Tech debt register** — add known issues to a `tech-debt/` subdirectory

The Research Enricher agent will search all files in this directory tree.
