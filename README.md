# chris-resume

Resume managed as code: canonical Markdown, reusable includes, CI builds.

## Quickstart

- Edit `src/resume.md` (target ≤ 2 pages, semantic Markdown).
- Build locally with Pandoc (requires Pandoc + XeLaTeX):

  ```bash
  mkdir -p output
  # Recommended PDF build: XeLaTeX + 1in margins + colored links
  pandoc src/resume.md \
    --pdf-engine=xelatex \
    -V geometry:margin=1in \
    -V colorlinks=true -V linkcolor=blue -V urlcolor=blue \
    -o output/resume.pdf

  # Also export HTML (standalone)
  pandoc src/resume.md -s -o output/resume.html
  ```

### PDF export tips

- Keep ≤ 2 pages by trimming content first (preferred), or slightly reduce margins if needed.
- If text spills onto a third page, try:

  ```bash
  pandoc src/resume.md --pdf-engine=xelatex -V geometry:margin=0.9in -o output/resume.pdf
  ```

- Optional customization: add a Pandoc/LaTeX template under `templates/` and pass `--template` or font variables for a different look.

## Structure

- `src/resume.md` — canonical résumé (publishable)
- `src/includes/` — reusable blocks (publishable)
- `src/roles/` — detailed role dossiers (keep factual and non-confidential)
- `work/` — local, git-ignored private scratch for temporary notes (NEVER committed)
- `.github/workflows/build.yml` — CI to produce PDF/HTML artifacts

## Tailoring Workflow

- Create a branch: `git checkout -b app/<company>-<role>`
- Tailor `src/resume.md` using the rules in `AGENTS.md`
- Push, open PR, and (optionally) tag: `git tag YYYY-MM-<company>-<role>`

## Privacy

- Treat this repo as public: no phone number, street address, or confidential details.
- Use `work/` for temporary private materials; do not copy raw content or sensitive metrics into `src/`.

## Private Working Docs

Create a local scratch area for confidential notes:

```bash
mkdir -p work
```

The `work/` directory is already listed in `.gitignore` and excluded from CI.
