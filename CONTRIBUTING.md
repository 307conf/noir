# Theme-specific contribution guidance — Hugo Noir (adapted for 307conf)

This file provides contributor-focused instructions specific to the Hugo Noir theme as it is used in this repository.

Why this exists
- The theme README is upstream and used by multiple projects. To avoid modifying upstream content directly here, this repository contains a theme-specific `CONTRIBUTING.md` with clear examples that match this site's conventions.

Key conventions (presentation & author pages)

1. Presentations (talks)
- Location: `content/<lang>/presentations/<slug>.md`
- Front matter format: **TOML** (`+++ ... +++`)
- Required/commonly used fields:
  - `title` (string)
  - `date` (ISO datetime)
  - `authors` (array of author slugs) — e.g. `authors = ["joao-vitor-keowu"]`
  - `location` (string)
  - `short_description` (string)
  - `summary` (string)
  - `logo` or `image` (path to speaker image)
  - `weight` (integer, optional)
- Optional override fields:
  - `speaker_name` (string) — override displayed name
  - `speaker_link` (string) — link to speaker page
  - `period` (string or datetime) — shown in lists; if absent, templates fallback to `site.Params.period`

Example (TOML):
```
+++
title = "Nome da apresentação"
date = 2025-12-13T10:00:00-03:00
authors = ["joao-vitor-keowu"]
period = "TDB"
location = "Sala 1"
short_description = "Breve descrição"
summary = "Resumo em mais detalhes"
logo = "/images/speakers/joao-vitor.png"
weight = 1
+++
```

2. Authors (speakers)
- Location: `content/<lang>/authors/<slug>.md`
- The `slug` referenced in `authors = ["..."]` should match the filename (without extension) or the explicit `slug` field in the author's front matter.

Example (TOML):
```
+++
title = "João Vitor (@keowu)"
description = "Short bio"
date = 2025-11-12T09:00:00-03:00
slug = "joao-vitor-keowu"
role = "Sr. Security Researcher"
+++
```

3. Global event period
- The site uses `params.period` in `hugo.toml` as a fallback when a page doesn't define `period`.
- Example in `hugo.toml`:
```
[params]
period = [
  2025-12-13T10:00:00-03:00,
  2025-12-14T18:00:00-03:00,
]
```

4. Archetypes
- Use the included archetypes to generate consistent front matter:
  - `hugo new pt-br/presentations/minha-palestra.md` will use `archetypes/presentation.md`.
  - `hugo new pt-br/authors/novo-autor.md` will use `archetypes/author.md`.

5. Checklist before opening a PR
- Use TOML front matter.
- Ensure `authors` references existing author slugs.
- Test locally with `hugo server -F` and check pages render correctly.
- Place images under `static/images/` and reference them with absolute paths `/images/...`.

If you want these same instructions copied into the theme README upstream, ask and I can prepare a PR to the original theme repository.
