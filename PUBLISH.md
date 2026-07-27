# Publishing Guide

> For environment setup and local development, see [README.md](README.md).  
> All commands below require the **venv to be active** (see [Prerequisites](README.md#prerequisites)).

## Overview

This project generates the [Conio SDK documentation site](https://sdk-docs.conio.com) using MkDocs and publishes it to GitHub Pages via [`mike`](https://github.com/jimporter/mike), which supports multiple documentation versions side by side.

The `docs/` folder in **main** always reflects the **latest** SDK version. Older versions are not kept in source — they are preserved as separate subdirectories in the `gh-pages` branch, built and frozen at publish time. Users can switch between versions using the selector in the site header.

Each published version corresponds to a **breaking release of the SDK** and is identified by a **version-name group** (e.g. `0.X.Y`, `2.5.X`). The alias `latest` always points to the most recently published version.

This guide covers three scenarios:

1. [Publish a new version](#1-publish-a-new-version) — when the SDK introduces breaking changes
2. [Update the latest version](#2-update-the-latest-version) — when an SDK update doesn't introduce breaking changes
3. [Update an older version](#3-update-an-older-version) — when a fix is backported to an older SDK version

See also: [Maintenance commands](#maintenance-commands) and [Troubleshooting](#troubleshooting).

---

## 1. Publish a new version

Use this when the SDK introduces **breaking changes** — i.e. changes that require existing integrations to be updated:

- Removed or renamed methods / classes / properties
- Changed method signatures (parameters added, removed, or reordered)
- Changed response types or error codes
- Behavioral changes that invalidate existing usage patterns

Follow the steps in [Update the latest version](#2-update-the-latest-version), using the **new** version-name group.

Do **not** create a new version for typo fixes, additive features, or formatting improvements — use the **existing** version-name group instead.

---

## 2. Update the latest version

Each documentation version lives on a dedicated branch (`docs/<version>`). Before publishing, that branch must be merged into `main` — `main` always reflects the current latest docs.

### Branch workflow

```sh
# Switch to the existing version branch...
git checkout docs/<version>
# ...or create one for a new version
git checkout -b docs/<version>

# Edit docs/ files, then push
git push origin docs/<version>

# Merge into main when ready
git checkout main
git merge --no-ff docs/<version>
git push origin main
```

### Preview locally

```sh
# Register the version locally (no push)
mike deploy <version> latest --update-aliases

# Serve the versioned site at http://127.0.0.1:8000
mike serve
```

Verify the new version renders correctly and the selector lists all expected versions before publishing.

### Publish

```sh
mike deploy --push --update-aliases <version> latest
```

---

## 3. Update an older version

Use this when a fix needs to be applied to an older published version. Each older version has its own branch (`docs/<version>`); changes there do not affect `main`.

### Branch workflow

```sh
git checkout docs/<version>
# Edit docs/ files, then push
git push origin docs/<version>
```

### Preview locally

```sh
mike deploy <version>
mike serve
```

### Publish

```sh
mike deploy --push <version>
```

The `latest` alias is not moved — only the content of that version is updated.

---

## Maintenance commands

```sh
# List all published versions and their aliases
mike list
```

---

## Troubleshooting

When running `mike deploy`, mike commits the built output to the local `gh-pages` branch and stops if there is nothing new to commit.

If you ran a **local preview** first, the local `gh-pages` branch already contains those changes, so `mike deploy --push` finds nothing to commit and skips the push.

**Fix:** hard-reset the last local commit on `gh-pages` to discard the preview build, then re-run `mike deploy --push`.

**WARNING:** before resetting, make sure the commit you are dropping has **not** been pushed to origin. **NEVER EVER** force-push to `gh-pages`.
