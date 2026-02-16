# Non-Functional Requirements Checklist

Use this checklist to ensure NFR coverage in every specification. Each category includes example requirements and suggested metrics.

---

## Performance

- [ ] **Response time:** Maximum acceptable latency for key operations (e.g. p95 < 200ms)
- [ ] **Throughput:** Requests per second the system must handle
- [ ] **Page load:** Time to first meaningful paint / largest contentful paint
- [ ] **Batch processing:** Maximum duration for background jobs
- [ ] **Database queries:** Maximum acceptable query execution time

**Metrics:** Latency percentiles (p50, p95, p99), requests/sec, Core Web Vitals

---

## Security

- [ ] **Authentication:** Method (OAuth 2.0, SAML, API keys) and session management
- [ ] **Authorisation:** Role-based access control (RBAC), resource-level permissions
- [ ] **Data encryption:** At rest (AES-256) and in transit (TLS 1.2+)
- [ ] **Input validation:** Protection against injection, XSS, CSRF
- [ ] **Audit logging:** Security-relevant events logged with sufficient detail
- [ ] **Secrets management:** How API keys, tokens, and credentials are stored
- [ ] **Vulnerability management:** Dependency scanning, penetration testing schedule

**Metrics:** Time to detect/respond to incidents, audit pass rate, CVE remediation SLA

---

## Accessibility

- [ ] **Standard:** WCAG 2.1 AA (minimum) or AAA
- [ ] **Keyboard navigation:** All functionality accessible without a mouse
- [ ] **Screen reader:** Semantic HTML, ARIA labels, logical tab order
- [ ] **Colour contrast:** Minimum 4.5:1 for normal text, 3:1 for large text
- [ ] **Motion:** Respect `prefers-reduced-motion`, no auto-playing animations
- [ ] **Alternative text:** All images and media have descriptive alt text
- [ ] **Error identification:** Errors clearly identified and described in text

**Metrics:** Automated accessibility scan score, manual audit findings, assistive technology test results

---

## Internationalisation (i18n)

- [ ] **Language support:** Which locales are supported at launch?
- [ ] **Text direction:** RTL support if applicable
- [ ] **String externalisation:** All user-facing strings in resource files
- [ ] **Date/time formats:** Locale-appropriate formatting
- [ ] **Number/currency formats:** Locale-appropriate formatting
- [ ] **Content expansion:** UI accommodates text length variation (German ~30% longer than English)
- [ ] **Character encoding:** UTF-8 throughout

**Metrics:** Locale coverage, untranslated string count, layout breakage per locale

---

## Scalability

- [ ] **Horizontal scaling:** Can the system add instances to handle load?
- [ ] **Data volume:** Expected growth rate and storage requirements
- [ ] **Concurrent users:** Peak concurrent user capacity
- [ ] **Rate limiting:** Thresholds and behaviour when exceeded
- [ ] **Caching strategy:** What is cached, TTL, invalidation approach

**Metrics:** Max concurrent users, response time under load, cost per transaction

---

## Reliability & Availability

- [ ] **Uptime target:** SLA percentage (e.g. 99.9% = 8.76h downtime/year)
- [ ] **Failover:** Automatic failover strategy and recovery time
- [ ] **Data durability:** Backup frequency, retention, and recovery testing
- [ ] **Graceful degradation:** Behaviour when dependencies are unavailable
- [ ] **Circuit breakers:** Protection against cascading failures

**Metrics:** Uptime %, MTTR, MTBF, RTO, RPO

---

## Observability

- [ ] **Logging:** Structured logging with correlation IDs
- [ ] **Metrics:** Key business and technical metrics exposed
- [ ] **Tracing:** Distributed tracing across service boundaries
- [ ] **Alerting:** Alert thresholds and escalation paths defined
- [ ] **Dashboards:** Operational dashboards for key health indicators
- [ ] **Error tracking:** Centralised error collection and grouping

**Metrics:** Mean time to detect (MTTD), alert noise ratio, dashboard coverage

---

## Maintainability

- [ ] **Code standards:** Linting, formatting, and review requirements
- [ ] **Documentation:** API docs, architecture decision records, runbooks
- [ ] **Test coverage:** Minimum coverage thresholds (unit, integration, e2e)
- [ ] **Deployment:** CI/CD pipeline, rollback capability, deployment frequency
- [ ] **Technical debt:** Tracking mechanism and remediation schedule

**Metrics:** Deployment frequency, lead time for changes, change failure rate

---

## Compliance & Legal

- [ ] **Data protection:** GDPR, CCPA, or relevant regulations
- [ ] **Data residency:** Where data is stored and processed
- [ ] **Retention:** Data retention and deletion policies
- [ ] **Consent:** User consent collection and management
- [ ] **Right to erasure:** Process for handling deletion requests
- [ ] **Audit trail:** Compliance-relevant actions logged immutably

**Metrics:** Compliance audit results, data subject request response time

---

## Usability

- [ ] **Consistency:** Follows design system and established patterns
- [ ] **Error handling:** Clear, actionable error messages
- [ ] **Loading states:** Feedback during asynchronous operations
- [ ] **Undo/recovery:** Users can recover from mistakes
- [ ] **Onboarding:** New user experience and documentation

**Metrics:** Task completion rate, error rate, time on task, SUS score
