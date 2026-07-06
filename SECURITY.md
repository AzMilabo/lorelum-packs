# Security Policy

## Supported versions

Lorelum Packs is in active early development. Content fixes are applied to the latest `main` branch only — there are no tagged release lines yet.

| Version | Supported |
|---------|-----------|
| `main` | ✅ |
| tagged releases | ✅ |

## Reporting a vulnerability

**Please do NOT report security issues via public GitHub issues.** Report them privately:

- 📧 Email: **security@lorelum.com**
- 🔒 Preferred: use [GitHub's private vulnerability reporting](https://github.com/AzMilabo/lorelum-packs/security/advisories/new)

Include if possible:
- A description of the issue and its potential impact
- The affected Practice / anti-pattern / template / decision (file path or id)
- Steps to reproduce or a concrete example
- Suggested fix (optional)

### Response timeline

| Step | Target |
|------|--------|
| Acknowledge receipt | within 48 hours |
| Initial assessment | within 5 business days |
| Fix or mitigation | depends on severity; we'll coordinate disclosure with you |

We follow **coordinated disclosure**. Once a fix is released, we'll credit you in the advisory unless you prefer to remain anonymous.

## Scope

This is a **content repository** (Markdown, YAML, templates) — there is no executable engine here. The security surface is therefore different from the main repo.

**In scope:**
- **Insecure or dangerous code samples** in Practices or templates that, if copied verbatim into a real project, introduce a vulnerability — e.g. patterns that bypass auth checks, mishandle secrets, or create injection risks.
- **Anti-patterns that mislead**: an anti-pattern entry whose detection guidance or framing could lead users *toward* an insecure pattern.
- **Decision-graph entries** (`decisions.yaml`) that recommend insecure choices without flagging the tradeoff.
- **Supply-chain risk in template dependencies**: a template that pins a known-vulnerable dependency or pulls from an untrusted registry.

**Out of scope (report elsewhere):**
- Vulnerabilities in the Lorelum CLI / retrieval engine / MCP server → [main repo security policy](https://github.com/lorelum/lorelum/blob/main/SECURITY.md).
- Vulnerabilities in third-party libraries referenced by code samples → report to the upstream maintainer. Our code samples are illustrative, not pinned production dependencies.
- Vulnerabilities in the SaaS platform / enterprise components → separate private repos.
- Social engineering, physical attacks, DoS.

## Security design notes

Knowledge-pack content gets injected into AI context and from there into real code. Treat any code sample in a Practice or template the way you'd treat a snippet from a stranger's blog: **review it before pasting it into production.**

Two specific risks content authors must guard against:

1. **Insecure-by-default samples.** A "how to call the API" sample that hardcodes a token, disables TLS verification, or constructs a URL by string concatenation teaches the AI to do exactly that. Author samples as you would production code.
2. **Security anti-patterns framed as solutions.** If a Practice recommends something with security tradeoffs (e.g. storing tokens in `localStorage`, client-side-only auth checks), the tradeoff must be called out explicitly and the anti-pattern side registered in `anti-patterns/index.yaml`.

The registry (in the main repo) will eventually ship quality scoring and sensitive-info scanning for packs, but **human review is the final gate** — there is no automated substitute for reading the content.
