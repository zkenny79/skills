---
name: security-audit
description: Perform security audits of codebases, configurations, and deployments. Use this skill when the user asks to audit security, check for vulnerabilities, review dependencies, scan for secrets, evaluate authentication/authorization, or assess overall security posture. Produces a structured security report with severity ratings and remediation steps.
---

# Security Audit

Perform systematic security audits that identify real vulnerabilities and misconfigurations. Focus on actionable findings with clear severity ratings and remediation steps.

## When to use this skill

- User asks to audit security of a project
- User asks to check for vulnerabilities or secrets
- User asks to review authentication/authorization
- User asks to evaluate dependency security
- User asks for a security posture assessment
- Before deployment or release of sensitive projects

## Audit Process

### 1. Scope Definition

Before auditing:

1. Identify what is in scope (codebase, configs, dependencies, deployment)
2. Understand the project's threat model (what data is sensitive, who are the actors)
3. Check if there are existing security policies or compliance requirements
4. Note the tech stack for targeted checks

### 2. Audit Categories

#### Secrets & Credentials

Scan for:
- Hardcoded API keys, tokens, passwords, or secrets in source code
- Secrets in environment files committed to version control
- Credentials in configuration files, Dockerfiles, or CI/CD configs
- Private keys, certificates, or signing keys in the repository
- Secrets in comments, docstrings, or test fixtures
- Base64-encoded secrets or obfuscated credentials

Check locations:
- All source files
- `.env`, `.env.local`, `.env.production` files
- `docker-compose.yml`, `Dockerfile`
- CI/CD configs (`.github/workflows/`, `.gitlab-ci.yml`)
- Config files (`config/`, `settings/`)
- Test files and fixtures

#### Dependency Security

Check for:
- Known vulnerabilities in dependencies (CVEs)
- Outdated dependencies with security patches available
- Dependencies from untrusted or abandoned sources
- Typosquatting risks (look-alike package names)
- Dependencies with excessive permissions or suspicious behavior
- Transitive dependency vulnerabilities

For each ecosystem:
- **Node.js**: Check `package.json` and `package-lock.json` for known vulns
- **Python**: Check `requirements.txt`, `Pipfile`, `pyproject.toml`
- **Go**: Check `go.mod` and `go.sum`
- **Rust**: Check `Cargo.toml` and `Cargo.lock`
- **Java**: Check `pom.xml`, `build.gradle`

#### Authentication & Authorization

Check for:
- Missing or weak authentication on sensitive endpoints
- Broken authorization (IDOR, privilege escalation paths)
- Session management issues (no expiration, insecure cookies)
- Password storage (must use bcrypt/argon2, never plaintext or MD5)
- JWT implementation issues (weak secrets, missing expiration, algorithm confusion)
- OAuth/OIDC misconfigurations
- Missing rate limiting on auth endpoints
- No account lockout after failed attempts

#### Input Validation & Injection

Check for:
- SQL injection (raw queries without parameterization)
- Command injection (shell exec with user input)
- XSS (unescaped output in web apps)
- Path traversal (file operations with user-controlled paths)
- SSRF (server-side requests with user-controlled URLs)
- Deserialization of untrusted data
- Missing content-type validation on uploads
- No file size limits on uploads

#### Configuration Security

Check for:
- Debug mode enabled in production
- Verbose error messages exposing stack traces
- CORS misconfiguration (wildcard origins with credentials)
- Missing security headers (CSP, HSTS, X-Frame-Options)
- Insecure TLS configuration
- Open S3 buckets or public cloud resources
- Default credentials in configs
- Unnecessary services or ports exposed

#### Data Protection

Check for:
- Sensitive data logged (passwords, tokens, PII)
- Unencrypted data at rest where encryption is expected
- Missing data classification
- PII handling without consent or retention policies
- Data in URLs or query parameters
- Sensitive data in analytics or tracking

#### Infrastructure & Deployment

Check for:
- Running as root in containers
- Missing resource limits in container orchestration
- Exposed internal services to the public internet
- Missing network segmentation
- Unpatched base images
- Secrets passed as environment variables in plain text
- Missing backup and recovery procedures

### 3. Severity Ratings

Use this classification:

| Severity | Description | Response Time |
|----------|-------------|---------------|
| **Critical** | Direct exploit possible, data breach likely, full system compromise | Immediate |
| **High** | Significant risk, requires specific conditions but likely exploitable | Within 24 hours |
| **Medium** | Moderate risk, requires multiple conditions or partial access | Within 1 week |
| **Low** | Minor risk, defense-in-depth improvement, unlikely to be exploited directly | Within 1 month |
| **Info** | Best practice recommendation, no direct risk | Next maintenance window |

### 4. Output Format

```markdown
# Security Audit Report

**Date**: YYYY-MM-DD
**Scope**: [what was audited]
**Auditor**: AI Agent

## Executive Summary

Brief overview of security posture and top concerns.

## Summary by Severity

| Severity | Count |
|----------|-------|
| Critical | X |
| High | X |
| Medium | X |
| Low | X |
| Info | X |

## Findings

### [CRITICAL] Title

- **Category**: Secrets / Auth / Injection / Config / etc.
- **Location**: file:line or component name
- **Description**: What the issue is
- **Evidence**: Code snippet or config showing the issue
- **Impact**: What an attacker could achieve
- **CVSS**: Estimated score if applicable
- **Remediation**: Specific steps to fix

### [HIGH] Title
...

## Positive Findings

Security practices that are well implemented.

## Recommendations

Prioritized list of improvements beyond specific findings.

## Methodology

Tools and techniques used in this audit.
```

### 5. Audit Principles

- **Be thorough but practical**: Focus on real risks, not theoretical edge cases
- **Provide evidence**: Show the exact code or config that is problematic
- **Suggest fixes**: Every finding must have a clear remediation path
- **Context matters**: A finding's severity depends on the project's threat model
- **Don't panic**: Present findings calmly with clear priorities
- **Verify assumptions**: Don't flag something as vulnerable without confirming the attack path
- **Respect sensitivity**: Handle any discovered secrets carefully, don't log them in reports

### 6. Automated Checks to Suggest

Recommend these tools for ongoing security:

- **Secrets**: git-secrets, trufflehog, gitleaks, detect-secrets
- **Dependencies**: npm audit, pip-audit, snyk, dependabot, renovate
- **Static analysis**: semgrep, codeql, sonarqube, bandit (Python), eslint-plugin-security
- **Container**: trivy, grype, docker scout
- **Infrastructure**: checkov, tfsec, scoutsuite, prowler
- **Web apps**: OWASP ZAP, burp suite, nikto
