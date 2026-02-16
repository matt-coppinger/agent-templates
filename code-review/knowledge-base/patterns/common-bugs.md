# Common Bug Patterns

Reference patterns for the bug scanner to check against. Organised by category.

## Null / Undefined Dereferences

### Pattern: Unchecked Optional Access
```
# Bad: accessing property without null check
user = get_user(id)
name = user.name  # crashes if user is None
```
**Fix**: Check for null/None before access, or use optional chaining.

### Pattern: Array Index Out of Bounds
```
# Bad: assuming array has elements
first = items[0]  # crashes if items is empty
```
**Fix**: Check length before access.

## Off-by-One Errors

### Pattern: Loop Boundary
```
# Bad: inclusive vs exclusive confusion
for i in range(1, len(items)):  # skips first element
```
**Fix**: Verify loop boundaries with edge cases (empty, single element, boundary).

### Pattern: String Slicing
```
# Bad: wrong substring boundary
substring = text[start:end-1]  # off by one
```

## Type Mismatches

### Pattern: String/Number Confusion
```javascript
// Bad: comparing string to number
if (statusCode == "200")  // loose equality, type coercion
```
**Fix**: Use strict equality (`===`) and consistent types.

### Pattern: Integer Division
```python
# Bad: integer division when float expected
average = total / count  # Python 2: integer division
```

## Race Conditions

### Pattern: Check-Then-Act
```python
# Bad: TOCTOU race condition
if os.path.exists(filepath):
    with open(filepath) as f:  # file could be deleted between check and open
```
**Fix**: Use try/except instead of check-then-act.

### Pattern: Shared Mutable State
```javascript
// Bad: concurrent modification without synchronisation
let counter = 0;
async function increment() {
    const current = counter;  // read
    await someAsyncWork();
    counter = current + 1;    // write — stale if another call ran
}
```
**Fix**: Use atomic operations or proper locking.

## Resource Leaks

### Pattern: Unclosed Connection
```python
# Bad: connection never closed on error
conn = database.connect()
result = conn.query(sql)  # if this throws, conn is never closed
conn.close()
```
**Fix**: Use context managers (`with`), `try/finally`, or RAII.

### Pattern: Event Listener Leak
```javascript
// Bad: adding listener without cleanup
useEffect(() => {
    window.addEventListener('resize', handler);
    // Missing: return () => window.removeEventListener('resize', handler);
});
```

## Error Handling Gaps

### Pattern: Swallowed Exception
```python
# Bad: silently ignoring errors
try:
    process_data(item)
except Exception:
    pass  # error silently lost
```

### Pattern: Missing Error Propagation
```go
// Bad: ignoring error return
result, _ := doSomething()  // error discarded
```

### Pattern: Partial Failure in Batch Operations
```python
# Bad: one failure stops entire batch, no rollback
for item in items:
    process(item)  # if item 50/100 fails, items 51-100 never processed
```
**Fix**: Collect errors per item, process all, report failures.

## Security Patterns

### Pattern: SQL Injection
```python
# Bad: string interpolation in SQL
query = f"SELECT * FROM users WHERE name = '{user_input}'"
```
**Fix**: Use parameterised queries.

### Pattern: Hardcoded Secrets
```
API_KEY = "sk-live-abc123..."
password = "admin123"
```
**Fix**: Use environment variables or secret management.

### Pattern: Path Traversal
```python
# Bad: user input in file path without sanitisation
filepath = os.path.join(upload_dir, user_filename)  # "../../../etc/passwd"
```
**Fix**: Validate and sanitise file paths, use allowlists.

## Performance Anti-Patterns

### Pattern: N+1 Query
```python
# Bad: query per item in loop
for user in users:
    orders = db.query("SELECT * FROM orders WHERE user_id = ?", user.id)
```
**Fix**: Batch query with `IN` clause or use eager loading.

### Pattern: Allocation in Hot Loop
```java
// Bad: creating objects in tight loop
for (int i = 0; i < 1000000; i++) {
    String key = new StringBuilder().append("prefix_").append(i).toString();
}
```
**Fix**: Reuse builders or pre-allocate outside the loop.
