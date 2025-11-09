# AGENTS.md

## Purpose

This document defines how AI assistants (“agents”) may read, interpret, and modify this repository.  
The goal is to enable résumé tailoring and automation **without ever exposing confidential, private, or proprietary information**.

Agents are expected to follow these instructions strictly when reading from or writing to files in this repository.

---

## Scope of Work

Agents may:

- Generate concise résumé variants, summaries, or formatting conversions (Markdown → PDF/HTML)
- Provide editing suggestions aligned with job descriptions or target roles
- Maintain tone, accuracy, and professional polish
- Propose patch diffs or edited file content; do not run git unless explicitly authorized by the human

Agents **must never**:

- Reveal, regenerate, or reconstruct any private data (e.g., full address, phone number, internal project names, non-public metrics)
- Output or publish raw internal notes, metrics, or role dossiers that contain company-sensitive or confidential content
- Introduce or invent details about the user’s employment history or performance

---

## Privacy and Confidentiality Rules

### ✅ Allowed Information

- Publicly shareable résumé content (titles, roles, years, skills, generic project descriptions)
- Quantified results that are **not** company-sensitive and do not imply internal metrics
- Industry-standard technology stacks (e.g., C++, Python, SystemC, etc.)
- Publicly verifiable career history already visible on LinkedIn or similar profiles

### 🚫 Prohibited Information

- Personal identifiers beyond:
  - **Name**
  - **Email** (professional)
  - **City/Region**
  - **LinkedIn or GitHub profile**
- **No** phone numbers, street addresses, or personal URLs not meant for public use
- **No** internal company names, code names, project numbers, or proprietary technology details
- **No** confidential metrics (revenue, sales, unreleased product data, client names)

---

## File Handling Rules

- `src/resume.md` is **publishable** and may be rewritten by agents.
- `src/includes/` is **publishable** and may be referenced or edited.

### Private Working Directory (never committed)

- `work/` at the repository root is a local, git-ignored scratch area for temporary notes, raw dumps, or potentially confidential source material.
- Agents may read documents in `work/` only to extract or summarize safe, public‑ready résumé content.
- Agents must never:
  - Copy or quote raw `work/` content verbatim into `src/` files or outputs.
  - Commit, list, or otherwise expose filenames or contents from `work/`.
  - Include confidential metrics, client names, internal code names, or unreleased data sourced from `work/`.

---

## Resume Output Guidelines

1. **Always write concise, factual, truthful content.**
2. **Target two pages maximum** (≈900–1200 words) for the main résumé.
3. **Tone:** Professional, direct, and outcome-driven — not self-promotional.
4. **Formatting:** Semantic Markdown.
5. **No hallucinated content.**

---

## Safe Prompt Template (for résumé tailoring)

```text
SYSTEM: You are a professional résumé editor. Follow the privacy and formatting rules in AGENTS.md.

USER INPUTS:
1. Target job description
2. Current canonical résumé (`src/resume.md`)
3. Optional contextual excerpts from `src/roles/` and `src/includes/`
  - Optional private inputs: selected excerpts from `work/` (never quoted verbatim; sanitize and generalize)
4. Constraints:
   - Keep ≤ 2 pages
   - Preserve factual accuracy
   - Do not introduce confidential details
   - Remove phone number and street address
   - Output valid Markdown ready for Pandoc

OUTPUT:
- Tailored résumé in Markdown format
- No extra commentary or non-Markdown text
- No git/branch/commit operations
```

---

## Verification Checklist

Before committing any AI-generated résumé to the repository:

| Check | Pass Criteria |
|-------|----------------|
| ✅ No PII | No phone, address, or non-public email |
| ✅ No confidential data | No client/internal project names or numbers |
| ✅ Proper format | Markdown only, ≤ 2 pages |
| ✅ No `work/` leakage | No raw quotes, filenames, or sensitive metrics from `work/` |
| ✅ Professional tone | Neutral, factual, impact-focused |
| ✅ No unauthorized VCS | No branch/commit/push/tag attempted |

---

## Agent Responsibilities

- Treat this repository as **public**.
- Follow `DESIGN.md` for repository structure and workflow.
- Annotate or summarize — do not fabricate.

---

## Operational Mode and VCS Policy

- Default: advisory and file-scoped. Provide proposed changes as diffs or full file contents.
- Do not create branches, commits, pushes, tags, or PRs unless explicitly requested by the human.
- Never modify git settings, credentials, or remotes.

---

## Revision Control

- Do not perform git operations unless explicitly instructed by the human.
- If asked to make commits/branches, use a **dedicated branch**:

  ```text
  app/<company>-<role>
  ```

- After review, tags may be created on request:

  ```text
  git tag YYYY-MM-<company>-<role>
  ```
  
- Never merge to `main` or push without explicit human approval.

---
