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
- `.github/workflows/build.yml` — CI to produce PDF/HTML artifacts

## Tailoring Workflow

- Create a branch: `git checkout -b app/<company>-<role>`
- Tailor `src/resume.md` using the rules in `AGENTS.md`
- Push, open PR, and (optionally) tag: `git tag YYYY-MM-<company>-<role>`

## Privacy

- Treat this repo as public: no phone number, street address, or confidential details.
