# Technical Writing Style Guide

Standards for all generated documentation. Every sub-agent must follow these rules.

## Language

- **Spelling:** British English throughout (colour, behaviour, initialise, serialise, centre, licence, analyse, categorise, organisation)
- **Voice:** Active voice preferred. "The function returns a user object" not "A user object is returned by the function."
- **Tense:** Present tense for descriptions. "This endpoint accepts a JSON body." Past tense only for changelogs.
- **Person:** Second person for tutorials and runbooks ("you"). Third person for API references ("the client").
- **Contractions:** Avoid in API references. Acceptable in tutorials.

## Structure

- **One idea per paragraph.** If a paragraph covers two concepts, split it.
- **Lead with the action.** Start steps with a verb: "Configure the database connection" not "The database connection should be configured."
- **Headings are scannable.** A reader should understand the document's content from headings alone.
- **Lists over prose** for sequential steps, options, or requirements.

## Code Examples

- Every public function or endpoint must have at least one example.
- Examples must be syntactically correct and runnable.
- Use realistic values, not `foo`, `bar`, `test123`.
- Show the expected output in a comment or separate block.
- Include error handling for non-trivial examples.
- Specify the language in fenced code blocks: ` ```python `, not ` ``` `.

## Formatting

- **Bold** for UI elements, field names, and key terms on first use.
- `Code font` for function names, parameters, file paths, and terminal commands.
- > Blockquotes for important warnings or notes.
- Tables for structured comparisons (parameters, error codes, config options).

## Tone

- Precise and concise. No filler words ("basically", "simply", "just", "actually").
- Respectful of the reader's time. Get to the point.
- Technical but accessible. Define acronyms on first use.
- No marketing language. "This function retrieves user data" not "This powerful function seamlessly retrieves user data."

## Common Mistakes to Avoid

| Wrong | Right |
|-------|-------|
| Initialize | Initialise |
| Color | Colour |
| Center | Centre |
| License (as noun) | Licence |
| Behavior | Behaviour |
| Organize | Organise |
| It's important to note that... | (Delete — just state the fact) |
| In order to | To |
| Utilize | Use |
| Functionality | Feature / capability |

## Cross-References

- Use relative paths for internal links: `[User type](../types/user.md)`
- Link type names to their definitions on first mention in a section.
- Mark external links: `[Express.js documentation](https://expressjs.com) (external)`
- Don't link the same term more than once per section.

## Versioning

- Include version badges at the top of API references.
- Mark deprecated items with: `> **Deprecated since v{X}.** Use [{alternative}]({link}) instead.`
- Changelog entries must include date, version, and a brief summary.
