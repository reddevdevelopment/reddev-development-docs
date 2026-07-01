# Publishing

This resource is ready to publish as a GitHub repository and connect to GitBook or another docs site.

## Current Docs Status

These documentation pages live in:

```text
https://github.com/reddevdevelopment/reddev-development-docs
```

They are intended to sync into:

```text
https://reddev-development.gitbook.io/reddev-development-docs
```

The full resource package is initialized as a local git repository on branch `main`.

No remote is configured yet for the resource package itself. The RedDev website repository was also found at:

```text
https://github.com/reddevdevelopment/reddev-development-site.git
```

Use a dedicated resource repository or GitHub release for the full package download because the zipped package is large.

## GitHub

Create or select a GitHub repository for the resource, then run these commands from the resource folder:

```powershell
cd "C:\Users\Cameron\Documents\Codex\2026-06-12\create-a-new-qbcore-resource-for\outputs\reddev_multicharacter"
git add .
git commit -m "Add RedDev Development reddev_multicharacter"
git remote add origin <YOUR_GITHUB_REPO_URL>
git push -u origin main
```

If GitHub CLI is installed and authenticated, Codex can help create the repo and push it.

## GitBook

GitBook can use this resource directly.

Recommended GitBook setup:

* Connect the GitHub repository.
* Set the docs root to `docs`.
* Use `docs/SUMMARY.md` for the sidebar.
* Use `docs/index.md` as the landing page.

The `.gitbook.yaml` file is already included at the resource root.

## GitDocs / Docs Site

For GitDocs, GitHub Pages, docsify, or similar static docs:

* Use `docs/index.md` as the main page.
* Use `docs/SUMMARY.md` as navigation if supported.
* Keep screenshots and media in a docs asset folder if added later.

Recommended publish paths:

* GitHub repo root for the resource.
* `/docs` for documentation.
* GitHub Pages source: `/docs` if using GitHub Pages.
