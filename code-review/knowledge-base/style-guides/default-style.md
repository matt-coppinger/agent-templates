# Default Style Guide

A general-purpose style guide for multi-language code review. Customise this file to match your team's conventions.

## Naming Conventions

### General Principles
- Names should be descriptive and unambiguous
- Avoid abbreviations unless universally understood (`id`, `url`, `http` are fine; `mgr`, `proc`, `cnt` are not)
- Longer scopes warrant longer names; loop counters may be single letters

### By Language Convention
- **Python**: `snake_case` for functions/variables, `PascalCase` for classes, `UPPER_SNAKE_CASE` for constants
- **JavaScript/TypeScript**: `camelCase` for functions/variables, `PascalCase` for classes/components, `UPPER_SNAKE_CASE` for constants
- **Java**: `camelCase` for methods/variables, `PascalCase` for classes, `UPPER_SNAKE_CASE` for constants
- **Go**: `camelCase` for unexported, `PascalCase` for exported, acronyms all-caps (`HTTPClient`, not `HttpClient`)
- **Rust**: `snake_case` for functions/variables, `PascalCase` for types/traits, `UPPER_SNAKE_CASE` for constants

### Boolean Variables
- Prefix with `is_`, `has_`, `should_`, `can_`, `will_` (or language-appropriate equivalent)
- Example: `is_valid`, `hasPermission`, `should_retry`

## Documentation

### Required Documentation
- All public functions, methods, and classes must have doc comments
- Module-level documentation for new files explaining purpose
- Complex algorithms must have inline comments explaining the approach
- API endpoints must document parameters, return types, and error codes

### Documentation Format
- Python: Google-style or NumPy-style docstrings
- JavaScript/TypeScript: JSDoc
- Java: Javadoc
- Go: Godoc conventions (comment starts with function name)
- Rust: `///` doc comments with examples

### What NOT to Document
- Obvious getter/setter methods
- Self-explanatory one-liner functions
- Implementation details that may change (document *what*, not *how*)

## Complexity

### Thresholds
- **Cyclomatic complexity**: warn at 10, critical at 20
- **Function length**: warn at 50 lines
- **Nesting depth**: warn at 4 levels
- **Parameter count**: warn at 5 parameters (consider an options object)
- **File length**: warn at 500 lines (consider splitting)

### Reducing Complexity
- Extract helper functions for nested logic
- Use early returns to reduce nesting
- Replace complex conditionals with named booleans or lookup tables
- Consider the strategy pattern for long switch/if-else chains

## Formatting

### General
- Consistent indentation (spaces preferred; match project convention)
- Maximum line length: 100-120 characters
- One blank line between functions, two between top-level sections
- No trailing whitespace

### Imports / Includes
- Group by: standard library → third-party → local
- Alphabetical within groups
- No wildcard imports in production code
- Remove unused imports

## Error Handling

### Principles
- Never swallow exceptions (empty catch blocks)
- Use specific exception types, not generic `Exception`/`Error`
- Always clean up resources (use `finally`, `defer`, `with`, or RAII)
- Log errors with sufficient context (what operation, what input, what failed)

### Anti-Patterns
- `catch (Exception e) {}` — silent failure
- Returning `null` instead of throwing on error
- Using exceptions for control flow
- Ignoring return values from functions that can fail

## Code Smells to Flag

- Magic numbers (use named constants)
- Dead code (unused variables, unreachable branches)
- Copy-pasted code (extract shared logic)
- God objects / functions (too many responsibilities)
- Premature optimisation (without profiling data)
- TODO/FIXME/HACK comments (track in issue tracker instead)
