# OpenClaw Security Guard

**Fast local security checks before you trust, install, or publish automation.**

`openclaw-security-guard` helps you scan prompts, shell commands, URLs, paths, and third-party skill folders for obvious security risks before they turn into expensive mistakes.

**Best for:** prompt/command safety checks, skill audits, secret leakage checks, and pre-publish guardrails.

---

# Why teams use it

- Catch common prompt-injection and exfiltration patterns early
- Review shell commands before automating them
- Block risky URLs and path traversal targets
- Audit third-party skill folders before install or publish
- Add a lightweight guardrail before ClawHub / GitHub releases

---

# What it checks

This repo supports fast local checks for:

- suspicious prompt text
- dangerous shell commands
- risky URLs (SSRF / localhost / metadata targets)
- unsafe file paths
- skill folders containing secrets, curl|bash patterns, destructive scripts, or exfiltration logic

---

# Verdicts

- `ALLOW` — no high-risk pattern found in this lightweight pass
- `WARN` — manual review required
- `BLOCK` — do not trust / run / publish until reviewed

A clean result means **no obvious pattern was detected**, not **the code is proven safe**.

---

# Install / Run

```bash
npm install
```

Quick checks:

```bash
node scripts/security-check.mjs text "<content>"
node scripts/security-check.mjs command "<shell command>"
node scripts/security-check.mjs url "<url>"
node scripts/security-check.mjs path "<path>"
```

Audit a skill / folder:

```bash
node scripts/audit-skill-dir.mjs /absolute/or/relative/path/to/skill
```

Write audit into Obsidian:

```bash
node scripts/write-obsidian-audit.mjs /tmp/audit.json "Skill Audit - my-skill"
```

Install local prepublish hook wrapper:

```bash
bash scripts/install-hooks.sh
```

---

# Typical use cases

- “Scan this prompt for prompt injection risk”
- “Check this shell command before automation”
- “Validate this URL / path”
- “Audit this third-party skill before install”
- “Add a security guard before publishing to ClawHub”

---

# Files

- `SKILL.md` — agent-facing routing and usage guidance
- `scripts/security-check.mjs` — text / command / URL / path checks
- `scripts/audit-skill-dir.mjs` — skill folder audit
- `scripts/write-obsidian-audit.mjs` — persist audit note to Obsidian
- `scripts/install-hooks.sh` — lightweight local install/publish wrapper
- `references/checklist.md` — audit categories and review philosophy

---

# Important limits

- This is a **lightweight guard**, not a sandbox
- Regex checks catch common patterns, not every attack
- High-risk code still needs human review and runtime isolation

---

# Bottom line

If you want a cheap, fast security layer before trusting external automation, this repo gives you a practical first-pass guard.
