# DESIGN.md

## Overview

This repository manages **Christopher P. Hurley’s résumé** as a versioned, structured, and reproducible project.  
It treats the résumé like source code — tracked, modular, and automatable — while maintaining professional privacy and LLM-friendly interfaces for tailoring job-specific variants.

The repository provides:

- A **canonical Markdown résumé** (`src/resume.md`)
- Detailed **per-role dossiers** under `src/roles/`
- Modular **include blocks** for reusable sections (`skills.md`, `projects.md`)
- **Continuous Integration (CI)** builds for PDF and HTML output
- An **LLM instruction guide** (`AGENTS.md`) for controlled automated edits
- This **design specification** (`DESIGN.md`) documenting all structure, rationale, and practices

---

## Objectives

1. **Single Source of Truth**  
   Keep one authoritative résumé file that can be tailored or exported without duplicating content.

2. **Structured Career History**  
   Preserve complete, detailed, and versioned records of each role for reference, future tailoring, and historical context.

3. **Automation and Portability**  
   Allow Pandoc-based builds (via GitHub Actions) to produce consistent PDF and HTML résumés across platforms.

4. **AI-Assisted Tailoring**  
   Enable safe, reproducible interaction with large language models using clear input boundaries and formatting expectations.

5. **Privacy and Professional Safety**  
   Avoid accidental leaks of personal or confidential company information while keeping enough transparency for public sharing.

---

## Directory Layout

```text
resume/
├─ src/
│  ├─ resume.md                 # canonical résumé (target ≤ 2 pages)
│  ├─ includes/                 # reusable, publishable content blocks
│  │  ├─ skills.md
│  │  └─ projects.md
│  ├─ roles/                    # detailed per-role dossiers (internal reference)
│  │  ├─ 2021-2025_solidigm_software_engineer.md
│  │  ├─ 2017-2021_intel_software_engineer.md
│  │  ├─ ...
├─ work/                        # local, git-ignored private scratch (NEVER committed)
├─ templates/                   # pandoc/typst/latex templates (optional)
├─ assets/                      # images (e.g., logo/headshot)
├─ output/                      # built résumé artifacts
├─ .github/workflows/
│  └─ build.yml                 # CI pipeline for PDF/HTML generation
├─ .gitignore                   # excludes output and sensitive data
├─ README.md                    # repo overview and usage
├─ AGENTS.md                    # LLM prompting and guardrails
├─ DESIGN.md                    # this document
└─ LICENSE                      # optional, MIT recommended
```

---

## Component Design

### 1. `src/resume.md`

- The **canonical résumé**.  
- Concise, up to two pages of Markdown designed for human readability and ATS (Applicant Tracking System) parsing.
- Maintains consistent formatting: `##` for section headings, `###` for roles, and bullet points (`-` or `*`) for accomplishments.
- Does **not** include full project or role detail — only summary bullet points suitable for publication.

### 2. `src/includes/`

- Houses **reusable blocks** (e.g., `skills.md`, `projects.md`, `summary.md`).
- Allows reuse of consistent wording across résumé variants.
- Encourages Markdown purity (no embedded HTML or styling).

### 3. `src/roles/`

- Each file is a **deep dive** into a specific role or position.
- Contains full context: scope, responsibilities, achievements, metrics, STAR stories, and links.
- Naming convention:

  ```text
  YYYY-YYYY_<company>_<short-role-title>.md
  ```

  Use underscores, lowercase, and four-digit years for lexicographic sort order.

- Recommended internal structure:

  ```markdown
  # Company – Title (Start–End)
  ## Scope
  Brief description: team size, tech stack, mission.

  ## Responsibilities
  - Concise list of owned areas or deliverables.

  ## Achievements
  - Measurable accomplishments (metrics, percentages, time savings).

  ## Notable Stories
  - Short STAR-style narratives for future bullet mining.

  ## Keywords
  comma-separated skill or domain tags.
  ```

### 4. `templates/`

- Stores Pandoc or Typst templates for résumé layout.
- Optional; can include typography, header/footer, or logo customization.

### 5. `output/`

- Contains built files (`resume.pdf`, `resume.html`).
- Auto-generated; **excluded from Git tracking** to keep history clean.

### 6. `.github/workflows/build.yml`

- Defines the CI/CD pipeline.
- Triggers on push or tag to build Markdown → PDF/HTML using Pandoc and TeXLive.
- Uploads build artifacts for download and optionally deploys to GitHub Pages.

### 7. `.gitignore`

- Ensures generated and private data never commit accidentally.

  ```gitignore
  /output/
  /build/
  *.log
  *.aux
  *.out
  *.toc
  ```

### 8. `AGENTS.md`

- Defines LLM usage guidelines for résumé tailoring:
  - What files to read (`src/resume.md`, selected `src/roles/*`, and includes)
  - Output constraints (≤ 2 pages, quantifiable bullets, no PII)
  - Tone and formatting standards
  - Example prompt template and verification checklist

### 9. `README.md`

- Human-readable summary of how to build and maintain the résumé.
- Should contain quickstart, build commands, and tagging conventions.

### 10. `DESIGN.md`

- Technical and architectural rationale (this file).
- Serves as the reference specification for any contributor or automation agent.

---

## Workflows

### Canonical Update

1. Edit `src/resume.md` directly to update your main résumé.
2. Commit to `main` branch.
3. CI automatically builds `output/resume.pdf` and `output/resume.html`.

### Application-Specific Tailoring

1. Create branch:  

   ```bash
   git checkout -b app/<company>-<role>
   ```

2. Use `AGENTS.md` to instruct an LLM to rewrite `src/resume.md` with relevant emphasis.
3. Commit and push changes.
4. Tag snapshot:

   ```bash
   git tag 2025-11-<company>-<role> && git push --tags
   ```

5. Download artifacts from CI or Releases.

### Role Documentation

- After each major milestone or job transition, add/update a dossier in `src/roles/`.
- Include metrics and stories while they’re fresh; keep these factual and internal.

### Privacy Workflow

- This repo is public:
  - Redact phone number and street address (keep city/region + LinkedIn).
  - Remove any internal project code names or confidential details.
  - Use `work/` for temporary private notes/dumps; never commit or quote raw contents.

### Private Working Notes

- Create a local `work/` directory for temporary, potentially confidential inputs.
- `work/` is git-ignored and excluded from CI. Treat as ephemeral; delete when no longer needed.
- When extracting into `src/resume.md`, sanitize language and avoid internal names/metrics.

---

## Build System

### Local Build

```bash
pandoc src/resume.md -o output/resume.pdf
pandoc src/resume.md -s -o output/resume.html
```

### GitHub Actions Build (Excerpt)

```yaml
name: Build resume
on:
  push:
    branches: [main]
    tags: ['*']
  workflow_dispatch:

jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - name: Install dependencies
        run: |
          sudo apt-get update
          sudo apt-get install -y pandoc texlive-latex-base texlive-latex-recommended texlive-fonts-recommended
      - name: Build resume
        run: |
          mkdir -p output
          pandoc src/resume.md -o output/resume.pdf
          pandoc src/resume.md -s -o output/resume.html
      - name: Upload artifacts
        uses: actions/upload-artifact@v4
        with:
          name: resume-build
          path: output/
```

---

## Versioning

- **Tags:** `YYYY-MM-<variant>` (e.g., `2025-11-swe`, `2026-01-pm`)
- **Branches:**
  - `main`: canonical résumé
  - `app/<company>-<role>`: tailored variants
- **Releases:** optional, attach PDFs for archiving

---

## Security and Privacy Notes

| Risk | Mitigation |
|------|-------------|
| Personal contact info | Publish only city, email, LinkedIn |
| Company IP / internal project names | Replace with descriptive generalizations |
| Accidental public leak of detailed roles | Keep repo private or exclude `/src/roles/` via `.gitignore` |
| LLM hallucination | Require adherence to `AGENTS.md` guardrails |
| Data loss | Treat GitHub as source of truth, export releases periodically |

---

## Tooling Rationale

| Tool | Purpose | Rationale |
|------|----------|-----------|
| **Markdown** | Authoring format | Lightweight, version-friendly, human-readable |
| **Pandoc** | Renderer | Flexible export (PDF, HTML, DOCX, etc.) |
| **LaTeX / Typst** | Typography engine | Professional PDF output |
| **GitHub Actions** | CI/CD | Consistent, automated builds |
| **Git** | Version control | Enables diffing, tagging, history |
| **LLM (Codex, GPT-5, etc.)** | Tailoring | Smart automation with human oversight |

---

## Maintenance and Lifecycle

| Frequency | Action |
|------------|--------|
| Quarterly | Review résumé for new achievements |
| After major project | Update relevant `src/roles/<role>.md` |
| Annually | Refresh skills, education, and contact info |
| As needed | Re-generate PDF/HTML and tag version |
| Continuous | Maintain `AGENTS.md` and `DESIGN.md` alignment |

---

## Future Enhancements

- [ ] Publish to GitHub Pages
- [ ] Integrate spellcheck/grammar lint via CI (`codespell`, `markdownlint`)
- [ ] Add automated résumé keyword matching (for job JD analysis)
- [ ] Introduce Typst-based theme for more elegant PDF
- [ ] Automate version changelog for résumé evolution

---
