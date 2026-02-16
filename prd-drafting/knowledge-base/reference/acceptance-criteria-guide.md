# Writing Good Acceptance Criteria

## The Given/When/Then Format

Acceptance criteria should follow the Given/When/Then (GWT) pattern, also known as Gherkin syntax. This format ensures criteria are structured, testable, and unambiguous.

### Structure

```
Given [precondition or context]
When  [action or event]
Then  [expected outcome]
```

### Example

```
Given I am logged in as a standard user with 3 items in my basket
When  I click the "Checkout" button
Then  I am redirected to the payment page showing all 3 items with correct totals
```

## Principles

### 1. Be Specific, Not Vague
❌ **Bad:** "The page should load quickly"
✅ **Good:** "Given a user on a 3G connection, when the dashboard loads, then the first meaningful paint occurs within 2 seconds"

### 2. One Behaviour Per Criterion
❌ **Bad:** "When I submit the form, it validates, saves, and sends an email"
✅ **Good:** Write three separate criteria — one for validation, one for saving, one for the email

### 3. Include Edge Cases
Don't just test the happy path. Consider:
- Empty states (no data, empty fields)
- Boundary values (maximum length, zero, negative numbers)
- Error states (network failure, invalid input, permission denied)
- Concurrent actions (two users editing the same record)

### 4. Make It Testable
Every criterion must be something a QA engineer can verify with a clear pass/fail outcome.

❌ **Untestable:** "The interface should be intuitive"
✅ **Testable:** "Given a new user who has never seen the application, when they complete the onboarding flow, then they can create their first project without external help within 5 minutes"

### 5. Avoid Implementation Details
Criteria describe *what*, not *how*.

❌ **Implementation:** "When the user clicks Save, the system makes a POST request to /api/projects"
✅ **Behaviour:** "When the user clicks Save, then the project appears in the project list within 2 seconds"

## Common Patterns

### Form Validation
```
Given I am on the registration form
When  I submit the form with an email address missing the @ symbol
Then  an inline error message "Please enter a valid email address" appears below the email field
And   the form is not submitted
```

### Permissions
```
Given I am logged in as a read-only user
When  I attempt to delete a report
Then  the delete button is not visible
```

### Asynchronous Operations
```
Given I have initiated a bulk export of 50 reports
When  the export is processing
Then  a progress indicator shows the percentage complete
And   I can continue using the application while the export runs
```

### Error Handling
```
Given I am submitting a payment
When  the payment gateway returns a timeout error
Then  the system displays "Payment could not be processed. Please try again."
And   no charge is applied to the user's account
And   the failed attempt is logged for investigation
```

## Anti-Patterns to Avoid

| Anti-Pattern | Problem | Fix |
|-------------|---------|-----|
| "Should work correctly" | Not testable | Define what "correctly" means |
| "Handle errors gracefully" | Vague | Specify each error and its handling |
| "Support all browsers" | Unbounded | List specific browsers and versions |
| "Be responsive" | Ambiguous (speed or layout?) | Specify breakpoints or response times |
| "Users can easily…" | Subjective | Define measurable ease (time, steps, error rate) |

## Checklist

Before finalising acceptance criteria, check:
- [ ] Is it in Given/When/Then format?
- [ ] Can a QA engineer write a test from this?
- [ ] Is there exactly one behaviour being tested?
- [ ] Are boundary/edge cases covered?
- [ ] Does it avoid implementation details?
- [ ] Is every term unambiguous?
- [ ] Could two people read this and agree on pass/fail?
