# Cybersecurity Engineer | Application Security | AI Security | DevSecOps

I work on finding security weaknesses in applications, APIs, cloud environments, CI/CD pipelines, and AI-assisted software — and, more importantly, fixing them.

My approach is practical: reproduce the issue, understand the root cause, implement the fix, add a security test, and make sure the same problem does not quietly come back later.

I am particularly interested in the security problems introduced by **AI-assisted software development**, where applications can be built extremely quickly but security decisions are often overlooked.

---

## What I Do

- Application & API Security
- Secure Code Review
- AI-Generated Code Security
- Vulnerability Assessment
- Penetration Testing
- DevSecOps & CI/CD Security
- Cloud Security
- Authentication & Authorization Security
- Dependency & Supply Chain Security
- Secrets Detection & Remediation
- Security Automation
- Python & JavaScript Security Tooling
- AI / LLM Application Security
- Security Testing & Vulnerability Remediation

I prefer engineering solutions over simply producing vulnerability lists.

A useful security assessment should answer:

> **What is wrong? Why is it happening? How can it be exploited? How should it be fixed? How do we prove the fix works?**

---

# Security Work & Real-World Patterns

Over the years, I have worked with the kinds of security problems that repeatedly appear in real applications and development environments.

Some examples of issues I have investigated and fixed include:

### Broken Access Control

An application correctly authenticated users but did not always verify whether the authenticated user was actually authorized to access the requested object.

For example:

```text
GET /api/orders/10452
```

Changing the object ID could expose another user's order when authorization was based only on authentication.

**Fix:** I introduced server-side ownership/authorization checks rather than relying on the object identifier supplied by the client.

> Authentication answers "Who are you?"
> Authorization answers "Are you allowed to do this?"
>
> Both need to be enforced independently.

---

### SQL Injection

I have encountered application code where user-controlled values were incorporated directly into database queries.

Unsafe pattern:
```python
query = "SELECT * FROM users WHERE email = '" + email + "'"
```

The correct approach is parameterized database access:
```python
cursor.execute(
    "SELECT * FROM users WHERE email = %s",
    (email,)
)
```

The important part is not simply changing one line of code. I also add regression tests so that the vulnerability does not return during a future refactor.

---

### Hardcoded Credentials & Secrets

Another recurring problem is credentials appearing in:
- Source code
- Configuration files
- `.env` files committed accidentally
- CI/CD configuration
- Debug output
- Deployment scripts

The remediation is more than deleting the value from the current file. A proper response can involve:
1. Revoking or rotating the exposed credential.
2. Checking repository history.
3. Removing the secret where appropriate.
4. Moving secrets into an appropriate secret-management mechanism.
5. Adding automated secret detection.
6. Reviewing where the credential was used.

---

### Insecure File Uploads

File upload functionality can become dangerous when an application trusts `filename`, `Content-Type`, or `file extension` without properly controlling what is actually uploaded and where it is stored.

Security controls I look for include:
- Allowlisted file types
- File size limits
- Randomized storage names
- Storage outside executable web directories
- Content validation
- Authorization checks
- Safe download handling
- Malware scanning where appropriate

---

### Command Injection

A particularly important pattern is application code passing user-controlled input into operating-system commands.

For example:
```python
os.system("ping " + user_input)
```

The safer design is generally to avoid shell interpretation and use a controlled API with strict validation and an allowlist where possible.

> If an application does not need to execute a shell command, don't give it a shell.

---

### Weak Authentication Implementations

I have also dealt with authentication implementations where security depended too heavily on client-side behavior or insufficient server-side validation.

Security review areas include:
- Password storage
- Session management
- Token validation
- Password reset flows
- Account enumeration
- Brute-force protection
- MFA enforcement
- Session expiration
- Logout/invalidation
- Privileged account controls

A login form looking secure does not necessarily mean the authentication system is secure.

---

### Dependency & Supply Chain Risks

Modern applications depend on hundreds or thousands of third-party packages.

I look for:
- Known vulnerable dependencies
- Abandoned packages
- Unnecessary dependencies
- Dependency confusion risks
- Unsafe package installation
- Uncontrolled version changes
- CI/CD dependency risks

Security is not only about the code your team writes. The software you depend on becomes part of your attack surface.

---

# AI-Generated Code Security

AI coding assistants have changed software development. They are extremely useful. They can also produce code that is:
- Functionally correct but insecure
- Overly permissive
- Missing authorization checks
- Vulnerable to injection
- Dependent on unnecessary packages
- Unsafe around filesystem operations
- Insecure in error handling
- Missing security tests
- Incorrectly implementing authentication

One of the areas I am actively exploring is:

## **"AI writes the code. Who checks the security?"**

My open-source work focuses on making that process easier.

---

# Featured Security Projects

## AI Code Security Scanner
**Repository:** `ai-code-security-scanner`

A developer-focused security scanner for identifying common security weaknesses in AI-assisted code.

### Planned capabilities
- SQL injection patterns
- Command injection
- Hardcoded secrets
- Dangerous filesystem operations
- Unsafe deserialization
- Weak authentication patterns
- Security-sensitive configuration
- Insecure dependency usage
- Missing security controls

The goal is not to claim that a scanner can prove software is secure. The goal is to identify suspicious patterns early and give developers useful remediation guidance.

---

## AI Security Fix Lab
**Repository:** `ai-security-fix-lab`

A collection of intentionally vulnerable applications demonstrating:

```text
Vulnerable Code -> Security Test -> Root Cause -> Secure Fix -> Regression Test
```

Each example focuses on understanding the vulnerability rather than simply copying a security checklist.

Examples include:
- SQL Injection
- Broken Access Control
- Command Injection
- XSS
- Insecure File Upload
- Authentication weaknesses
- SSRF
- Sensitive information exposure
- Unsafe AI output handling

All demonstrations use isolated test environments and synthetic data.

---

## AI Code Security Benchmark
**Repository:** `ai-code-security-benchmark`

A reproducible benchmark for evaluating security-analysis techniques against known vulnerable examples.

The project focuses on:
- Detection coverage
- False positives
- False negatives
- Precision
- Recall
- Runtime
- Vulnerability category coverage

Security tooling should be measured, not simply advertised.

---

## AI Secrets Guardian
**Repository:** `ai-secrets-guardian`

A security-focused project for detecting potentially exposed credentials and sensitive configuration before they reach source control or production.

```text
Possible API Key
File: config/settings.py
Line: 24
Value: [REDACTED]
Recommended: Rotate -> Remove -> Review History -> Secure Storage
```

Secrets should never be printed in security reports simply because a scanner found them.

---

## AI Agent Security Toolkit
**Repository:** `ai-agent-security-toolkit`

Security testing and hardening utilities for applications where AI models can interact with tools, APIs, files, databases, or other systems.

Areas of interest include:
- Excessive permissions
- Prompt injection
- Tool authorization
- Unsafe tool arguments
- Sensitive information exposure
- Human approval for high-risk operations
- Sandboxing
- Audit logging
- Resource restrictions

An AI agent should not receive more authority than it actually needs.

---

## Secure AI Development Workflows
**Repository:** `secure-ai-dev-workflows`

Security-focused GitHub Actions and development workflow examples covering:
- SAST
- Dependency scanning
- Secret detection
- Security tests
- Pull-request checks
- Least-privilege workflow permissions
- CI/CD hardening

The objective is to move security closer to the development process instead of waiting until production.

---

# Security Engineering Philosophy

```text
Understand -> Reproduce -> Measure -> Fix -> Test -> Automate -> Monitor
```

Finding a vulnerability is only part of the job. If the development team cannot understand the issue, reproduce it, fix it, and prevent regression, the security work is incomplete.

---

# Technologies & Tools

### Programming
`Python` `JavaScript` `TypeScript` `SQL` `Bash`

### Application Security
`OWASP` `SAST` `DAST` `API Security` `Secure Code Review`

### Security Testing
`Burp Suite` `Nmap` `Semgrep` `Bandit` `OWASP ZAP`

### DevSecOps
`Git` `GitHub Actions` `CI/CD` `Docker` `Security Automation`

### Cloud & Infrastructure
`Linux` `Docker` `Cloud Security` `Secrets Management`

### AI Security
`LLM Security` `Prompt Injection` `AI Agents` `RAG Security` `AI-Assisted Development`

> Tools are only useful when combined with sound security reasoning. I focus on understanding the underlying vulnerability rather than relying blindly on scanner output.

---

# How I Approach a Security Finding

### 01 - Identify
Find suspicious behavior through code review, automated analysis, testing, or monitoring.

### 02 - Validate
Determine whether the finding is actually exploitable or represents a genuine security weakness.

### 03 - Understand
Trace the vulnerability back to its root cause.

### 04 - Remediate
Implement a secure solution appropriate to the application's architecture.

### 05 - Test
Create or update security tests to verify the fix.

### 06 - Prevent
Add automation, CI/CD checks, coding standards, or monitoring where appropriate.

---

# Available for Security Work

I am available for selected security engineering and consulting work involving:
- Application security reviews
- API security assessments
- Secure code reviews
- AI-generated code security reviews
- AI/LLM application security
- Vulnerability remediation
- DevSecOps implementation
- CI/CD security
- Security automation
- Security testing

If you have an application, API, AI system, or development pipeline that needs a security review or remediation work, feel free to reach out.

## WhatsApp
**+92 316 7417135**

---

### Security First. Evidence Over Assumptions. Fixes Over Findings.

*Security testing should only be performed against systems where appropriate authorization has been obtained.*

---

## TODO
- [ ] Replace generic "I have encountered" examples with 5-10 real security issues personally fixed
- [ ] Create profile README repo (mhamidlad/mhamidlad) and push this
- [ ] Verify all listed tools are genuinely known before publishing
