# chris-resume

Resume managed as code: canonical Markdown, reusable includes, CI builds.

## Quickstart

- Edit `src/resume.md` (target ≤ 2 pages, semantic Markdown).
- Build locally with Pandoc:

  ```bash
  mkdir -p output
  pandoc src/resume.md -o output/resume.pdf
  pandoc src/resume.md -s -o output/resume.html
  ```

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
