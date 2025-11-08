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
4. Constraints:
   - Keep ≤ 2 pages
   - Preserve factual accuracy
   - Do not introduce confidential details
   - Remove phone number and street address
   - Output valid Markdown ready for Pandoc

OUTPUT:
- Tailored résumé in Markdown format
- No extra commentary or non-Markdown text
```

---

## Verification Checklist

Before committing any AI-generated résumé to the repository:

| Check | Pass Criteria |
|-------|----------------|
| ✅ No PII | No phone, address, or non-public email |
| ✅ No confidential data | No client/internal project names or numbers |
| ✅ Proper format | Markdown only, ≤ 2 pages |
| ✅ Professional tone | Neutral, factual, impact-focused |

---

## Agent Responsibilities

- Treat this repository as **public**.
- Follow `DESIGN.md` for repository structure and workflow.
- Annotate or summarize — do not fabricate.

---

## Revision Control

- Any modification by an agent must occur in a **dedicated branch**:

  ```text
  app/<company>-<role>
  ```

- After review, changes may be merged or tagged with:

  ```text
  git tag YYYY-MM-<company>-<role>
  ```
  
- Agents should not merge to `main` without human approval.

---
