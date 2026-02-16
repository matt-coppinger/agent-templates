# Technical Specification: [Title]

**Author:** [Name]
**Date:** [Date]
**Version:** [Version]
**Status:** Draft | In Review | Approved
**Related PRD:** [Link or ID]

---

## 1. Overview

### Context
[Why this technical work is needed. Reference the PRD or feature brief.]

### Objective
[What this spec aims to achieve technically.]

### Scope
[What is and is not covered by this technical spec.]

---

## 2. System Design

### Architecture
[High-level architecture. Include diagram if helpful.]

```
[ASCII diagram or reference to external diagram]
```

### Components
| Component | Responsibility | Technology |
|-----------|---------------|------------|
| [Name] | [What it does] | [Stack/framework] |

### Data Flow
[Describe how data moves through the system for the key operations.]

---

## 3. API Design

### New Endpoints

#### `[METHOD] /path`
**Description:** [What it does]

**Request:**
```json
{
  "field": "type — description"
}
```

**Response:**
```json
{
  "field": "type — description"
}
```

**Error Codes:**
| Code | Description |
|------|-------------|
| 400 | [Reason] |
| 404 | [Reason] |

### Modified Endpoints
[Any changes to existing endpoints.]

---

## 4. Data Model

### New Tables/Collections

```sql
CREATE TABLE example (
    id UUID PRIMARY KEY,
    -- fields
    created_at TIMESTAMP NOT NULL DEFAULT NOW()
);
```

### Schema Changes
[Modifications to existing tables. Include migration strategy.]

### Data Migration
[If applicable, describe the migration plan and rollback strategy.]

---

## 5. Non-Functional Requirements

| Category | Requirement | Target | Validation |
|----------|-------------|--------|------------|
| Performance | [e.g. Response time] | [e.g. < 200ms p95] | [Load test] |
| Scalability | [e.g. Concurrent users] | [e.g. 10k simultaneous] | [Stress test] |
| Security | [e.g. AuthN/AuthZ] | [e.g. OAuth 2.0 + RBAC] | [Security review] |
| Availability | [e.g. Uptime] | [e.g. 99.9%] | [Monitoring] |

---

## 6. Dependencies

| Dependency | Team/System | Status | Risk if Delayed |
|-----------|-------------|--------|----------------|
| [Name] | [Owner] | [Ready/In Progress/Blocked] | [Impact] |

---

## 7. Testing Strategy

### Unit Tests
[Key areas for unit test coverage.]

### Integration Tests
[Integration points to test.]

### End-to-End Tests
[Critical user flows to validate.]

### Performance Tests
[Load/stress testing approach.]

---

## 8. Rollout Plan

### Feature Flags
[Any feature flags for gradual rollout.]

### Phases
| Phase | Scope | Rollback Trigger |
|-------|-------|-----------------|
| 1 | [e.g. Internal dogfood] | [Condition] |
| 2 | [e.g. 10% of users] | [Condition] |
| 3 | [e.g. General availability] | [Condition] |

### Monitoring
[Key metrics and alerts to set up.]

---

## 9. Risks and Mitigations

| Risk | Likelihood | Impact | Mitigation |
|------|-----------|--------|------------|
| [Description] | High/Medium/Low | High/Medium/Low | [Strategy] |

---

## 10. Open Questions

| # | Question | Owner | Status |
|---|----------|-------|--------|
| 1 | [Question] | [Name] | Open |

---

## 11. Appendices

### A. Glossary
| Term | Definition |
|------|-----------|
| [Term] | [Definition] |

### B. References
- [Links to related specs, documentation, design docs]
