---
name: memory-digest-rules
description: Shared vault-writing rules for memory-digest-daily and memory-digest-spec sub-agents.
---

# Vault-Writing Rules — Shared by Digest Sub-agents

---

## Granularity filter — vault purpose

The vault documents **how to generate quality code**: patterns, conventions, architectural decisions, and non-obvious constraints. It is not a mirror of the codebase.

Before promoting any item, ask: *"Does this help someone write better code in the future, or does it just describe what the code looks like right now?"*

- If it helps write better code → promote it as a reusable pattern or decision rationale.
- If it only describes current code state (field types, enum values, method parameters, step-by-step task lists) → discard it. That lives in source files and git history.

---

## Write to vault

> **Writing convention:** All vault content must follow the `obsidian-vault` skill — YAML frontmatter, kebab-case filenames, wikilink format, and section structure. The skill was invoked in Step 1; apply its rules when writing every document.

For each classified item:

1. **Check for duplicates first** — use `Grep` to verify the concept is not already documented.
2. **Update existing documents** when the concept is already there — add a sub-section or table row; never create a duplicate file.
3. **Create new documents** when the topic is genuinely new: choose the vault section that best fits (use Step 3's classification table as a guide), name the file following `obsidian-vault` skill rules (kebab-case filename, YAML frontmatter with `title` and `summary`), and structure it with clear headings, organized sections, and tables or lists — curate, do not dump raw notes.
4. **Apply bidirectional Obsidian links** (`[[Section/Document]]`) — new notes must link to related documents, and related documents must link back.
5. **Language:** maintain the vault's established language (check existing vault documents — typically whatever language is already in use).
6. **Placement:** always use full path relative to vault root (e.g., `[[Decisions/ADR - Security]]`), not bare filenames.

---

## Update indexes

If new vault documents were created:

- Add entry to `docs/vault/Home.md` in the correct section.
- Add entry to `docs/vault/Decisions/Index.md` if a decision was recorded.
- Evaluate if `.claude/commands/conditional-docs.md` needs a new condition (only when the new document should be read before touching specific files/paths).

---

## Update skills

Skills live in `.claude/skills/<name>/SKILL.md`. If any extracted knowledge belongs in a skill, update it — this is as important as updating the vault.

**How to find skills:** `Glob` with pattern `.claude/skills/*/SKILL.md`.

**When to update a skill:**
- A new reusable pattern was discovered.
- A recurring mistake was corrected and the correct approach should be codified.
- A gotcha specific to a technology layer was found.
- A new standard was established.

**When NOT to update a skill:**
- The knowledge is purely business/domain-specific (→ vault ADR or PRD).
- The knowledge is infrastructure/deployment (→ `docs/vault/Architecture/`).
- The pattern is already in the skill — always `Grep` the `SKILL.md` before writing.

**How to update:**
1. Read the relevant `SKILL.md` to find the correct section.
2. Add the new pattern, rule, or anti-pattern consistently with existing content.
3. If a pattern contradicts existing content, update it — never leave conflicting guidance.

---

## Evaluate Claude Rule

If a new vault document is linked to a specific folder, file, or file type in the repo:

- Check if a Claude Rule already exists for that path in `.claude/rules/`.
- If not, create `.claude/rules/<kebab-case-name>.md`:

```markdown
---
paths:
  - 'path/to/folder/**/*'
---

# Descriptive Name

## Mandatory reading

Before creating or modifying files in `<path>`, read:

- `docs/vault/<Section>/<Document>.md` — one-line description.

## Mandatory documentation update

When creating, modifying, or deleting files in `<path>`:

1. Reflect changes in `docs/vault/<Section>/<Document>.md` in the same commit.
```

---

## Shared critical rules

- Never promote secrets, credentials, or sensitive data to the vault.
- Never duplicate information already in the vault — always `Grep` before writing.
- Bidirectional links are mandatory — an isolated vault document loses value.
