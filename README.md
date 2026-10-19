# GRID project website

Public website for the Global RIver-lanD (GRID) project, built with Quarto and served at https://grid-db.github.io.

## Preview and build

Install [Quarto 1.5.49](https://github.com/quarto-dev/quarto-cli/releases/tag/v1.5.49), the version pinned in the publishing workflow. The current pages need no R or Python execution environment.

From this repository:

```sh
quarto preview --no-browser
quarto render
```

The render output is `_site/`, which is ignored by Git. Check desktop and narrow-screen layouts, navigation, search, image descriptions, and local links before publishing. Preview serves local content; it does not publish it.

## Content map

- `index.qmd`, `about.qmd`, `development.qmd`: project introduction and proposed GRID-SI roadmap.
- `database/`: access, coverage, methods, contributions, and individual releases.
- `people/people.qmd`: current working group, core proposal team, and advisers.
- `education/` and `events/`: teaching resources and dated research updates. The IAMG 2026 river-chemistry module has its own Education page with Colab, repository, and instructor-guide links.
- `_variables.yml`: the single source for the dated GRID inventory totals. Update the date and numbers together only after checking the underlying inventory.
- `_review/`: unpublished policy draft and editorial/source notes. This directory is ignored by Git and excluded from rendering. It must never be linked as a public resource. Publish a policy only after its final text is explicitly approved; never force-add private review material.

Retain existing URLs where possible. Each research output should identify its specific scope, repository DOI, credited creators, date, and reuse terms. Whole-GRID totals are distinct from any individual release. Separate existing resources from proposed work; never imply funding or completed services from a proposal alone.

## Publish after GitHub sync

Every push to `main` triggers **Quarto Publish**. It renders the site and writes the result to `gh-pages`; GitHub Pages serves the root of that branch. A manual run is also available in GitHub Actions, restricted to `main`.

Local saves, local commits, clones, and pulls do not publish. A sync that pushes commits to `main` does. Publishing requires the repository's existing Actions and Pages permissions.

The workflow serializes publishing: an active run finishes, and only the latest pending update is retained. Rapid pushes can therefore combine into the latest pending deployment rather than deploying every intermediate commit. Quarto is pinned to 1.5.49; test a full render before changing that version.

After an approved push:

1. In [Actions](https://github.com/grid-db/grid-db.github.io/actions/workflows/publish.yml), verify that **Quarto Publish** succeeded for the exact pushed source commit.
2. Verify that the resulting GitHub Pages deployment succeeded. A failed render does not publish new output; a successful render alone does not prove the Pages deployment succeeded.
3. Open https://grid-db.github.io and verify the expected page changes, links, and images.

Do not edit generated files on `gh-pages` or manually copy `_site/` into the source branch. See [Quarto's publishing documentation](https://quarto.org/docs/publishing/github-pages.html#github-action).
