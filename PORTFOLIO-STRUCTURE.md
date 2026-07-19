# Portfolio structure — suggestion

This is a suggested structure for a dedicated portfolio repository (e.g. `technical-writing-portfolio`), so recruiters can navigate your work in under 2 minutes.

## Why a dedicated repo (instead of scattered ones)

Right now the samples live in separate repositories with Portuguese names
(`Como-cadastrar-uma-chave-PIX`, `Cases`, `Formacao-e-Cursos`...). An international
recruiter has no context for what each one is, and won't spend time clicking
into each to find out. One repository, in English, with a clear index, solves
that in a single visit.

## Suggested repo layout

```
technical-writing-portfolio/
├── README.md              → index page (see PORTFOLIO-INDEX-TEMPLATE.md)
├── api-reference/
│   └── change-status-api.md
├── how-to-guides/
│   └── register-a-pix-key.md
├── release-notes/
│   └── sample-release-notes.md
├── case-studies/
│   └── choosing-a-solution.md
└── style-guide/
    └── writing-guidelines.md
```

## Rules for each sample

1. **Everything in English.** File names, headings, content, commit messages.
2. **Keep the original Portuguese version too**, if you want — as
   `register-a-pix-key.pt-br.md` — it shows range, but the English version
   should always be the default/first one a visitor sees.
3. Each doc should open with 1–2 lines of context: what it is, who it's for,
   what tool/process was used to produce it (this is what proves Docs-as-Code
   fluency, not just writing ability).
4. Where possible, include a short **before/after** or **problem/solution**
   note — recruiters evaluating Technical Writers care about your process,
   not just the polished output. See `case-studies/` for a template.

## Repo metadata checklist

For the main profile repo and this portfolio repo:

- [ ] Add a one-line **description** (top right of repo page)
- [ ] Add **topics**: `technical-writing`, `docs-as-code`, `markdown`, `documentation`
- [ ] Remove personal phone number from any public file
- [ ] Add a link to this portfolio repo in the profile README
