# Security Policy — Spudich Lab

This policy applies to **every repository** in the `SpudichLab` organization. It
exists so lab members who aren't software engineers can write and ship code
(often with Claude Code) behind a good-enough security guardrail, and so the
lab's intellectual property stays protected.

## Reporting a vulnerability or leak

Email the org owner: **jongmin.sung@gmail.com**. Do **not** open a public issue
for a suspected secret leak or vulnerability — report it privately so the key can
be rotated / the bug fixed before it's disclosed.

## What is scanned automatically

Every repo runs these checks for you — you don't have to remember to run them:

| Check | Tool | Catches | Where results show |
|---|---|---|---|
| Code vulnerabilities | GitHub CodeQL (default setup) | ReDoS, injection, unsafe eval, path traversal | **Security** tab, PR checks |
| Secrets / keys | GitHub Secret Protection + gitleaks (CI) | API keys, tokens, passwords committed by mistake | Push protection + **Actions** |
| Dependency CVEs | pip-audit (CI) | known-vulnerable Python packages | **Actions** (informational) |

A **red secret-scan or code-scanning check must be fixed before merging.** The
easiest fix path: ask Claude Code to resolve the finding, or ping the org owner.

## The IP redline (most important)

Per spud-drug `docs/adr/0005-knowledge-ip-governance.md`:

- **Never commit** NDA / partner-confidential data, unpublished compound names,
  internal program names, or raw assay results. Public + lab-derived knowledge
  and synthesized ideas are free.
- **Never paste** any of the above into third-party tools (paperclip, web search,
  external LLMs) — those queries leave the lab. Public terms only.
- Tag knowledge pages `confidentiality: public | lab | nda-<partner>`; `nda-*`
  data belongs in its partner silo, never a shared repo.
- Secrets (`.env`, keys, tokens) never go in git. Read them from environment
  variables and keep the file gitignored.

## If you use Claude Code

Each repo carries a `.claude/rules/security.md` that makes Claude Code check for
these issues before every commit. You can also run `/security-review` at any time
to review your pending changes.
