# {SYSTEM_NAME} Architecture Document

> **Version:** {VERSION}
> **Last updated:** {DATE}
> **Status:** {Draft/Review/Approved}
> **Owner:** {TEAM_NAME}

## Overview

{High-level description of the system, its purpose, and key capabilities.}

## Context

{Where this system sits in the broader organisation. Who uses it and why.}

### System Context Diagram

```mermaid
{context diagram showing external actors and systems}
```

## Architecture

### Component Diagram

```mermaid
{component diagram showing internal structure}
```

### Components

#### {Component Name}

- **Purpose:** {What it does}
- **Technology:** {Language, framework, runtime}
- **Owns:** {Data or resources it manages}
- **Depends on:** {Other components or services}

## Data Flow

{How data moves through the system, from input to output.}

### Sequence Diagram: {Key Flow Name}

```mermaid
{sequence diagram for primary flow}
```

## Data Model

{Key entities, their relationships, and storage.}

| Entity | Storage | Owner | Description |
|--------|---------|-------|-------------|
| {entity} | {database/cache/queue} | {component} | {description} |

## Infrastructure

{Deployment topology, environments, and key infrastructure components.}

| Environment | Purpose | URL |
|-------------|---------|-----|
| {env} | {purpose} | {url} |

## Security

{Authentication, authorisation, encryption, and data protection.}

- **Authentication:** {method}
- **Authorisation:** {model — RBAC, ABAC, etc.}
- **Encryption:** {at rest and in transit}
- **Data classification:** {public, internal, confidential, restricted}

## Architecture Decisions

### ADR-{N}: {Decision Title}

- **Status:** {Proposed/Accepted/Deprecated/Superseded}
- **Context:** {Why this decision was needed}
- **Decision:** {What was decided}
- **Consequences:** {Trade-offs and implications}

## Non-Functional Requirements

| Requirement | Target | Current | Notes |
|-------------|--------|---------|-------|
| Availability | {target} | {current} | {notes} |
| Latency (p99) | {target} | {current} | {notes} |
| Throughput | {target} | {current} | {notes} |
| Recovery time | {target} | {current} | {notes} |

## Known Limitations

- {Limitation 1 and any planned mitigation}
- {Limitation 2}

## Changelog

| Date | Version | Author | Changes |
|------|---------|--------|---------|
| {date} | {version} | {author} | {summary} |
