# Security Review Checklist

Use this checklist when scanning code changes for security vulnerabilities.

## 1. Secrets & Credentials

- [ ] No hardcoded API keys, tokens, or passwords
- [ ] No secrets in configuration files committed to VCS
- [ ] Secrets loaded from environment variables or secret manager
- [ ] No secrets in log output or error messages
- [ ] `.env` files in `.gitignore`

## 2. Input Validation

- [ ] All user input validated and sanitised
- [ ] SQL queries use parameterised statements (no string interpolation)
- [ ] HTML output escaped to prevent XSS
- [ ] File paths validated against traversal attacks (`../`)
- [ ] URL parameters validated before use in redirects (open redirect)
- [ ] JSON/XML parsing has size limits (denial of service)
- [ ] Regular expressions checked for ReDoS vulnerability

## 3. Authentication & Authorisation

- [ ] Authentication required for protected endpoints
- [ ] Authorisation checked (not just authentication) — user can access *this* resource
- [ ] No broken object-level authorisation (IDOR)
- [ ] Session tokens generated with cryptographic randomness
- [ ] Password handling uses bcrypt/scrypt/argon2 (not MD5/SHA1)
- [ ] Rate limiting on authentication endpoints

## 4. Data Exposure

- [ ] Sensitive data not returned in API responses unnecessarily
- [ ] Error messages don't leak internal details (stack traces, DB schemas)
- [ ] Logging doesn't include PII or sensitive data
- [ ] Debug endpoints disabled in production
- [ ] CORS configured restrictively (not `*`)

## 5. Dependencies

- [ ] No known vulnerable dependency versions
- [ ] Lock files committed (`package-lock.json`, `Pipfile.lock`, etc.)
- [ ] Third-party code reviewed before inclusion
- [ ] Subresource integrity for CDN assets

## 6. Cryptography

- [ ] Using standard libraries (not custom crypto)
- [ ] TLS for all external communications
- [ ] Adequate key sizes (RSA ≥ 2048, AES ≥ 128)
- [ ] No deprecated algorithms (MD5, SHA1 for security, DES)
- [ ] Random values from cryptographic PRNG (`crypto.randomBytes`, not `Math.random`)

## 7. Error Handling & Logging

- [ ] Errors handled gracefully (no crash on malformed input)
- [ ] Failed operations don't leave system in inconsistent state
- [ ] Security events logged (failed auth, permission denied, invalid input)
- [ ] Log injection prevented (user input not interpolated into log format strings)

## 8. Infrastructure & Configuration

- [ ] No debug flags enabled in production config
- [ ] Security headers set (CSP, HSTS, X-Frame-Options)
- [ ] File upload restrictions (type, size, storage location)
- [ ] Temporary files cleaned up
- [ ] Least privilege principle for service accounts and IAM roles

## Common References

- **OWASP Top 10**: https://owasp.org/www-project-top-ten/
- **CWE Top 25**: https://cwe.mitre.org/top25/
- **OWASP ASVS**: https://owasp.org/www-project-application-security-verification-standard/
