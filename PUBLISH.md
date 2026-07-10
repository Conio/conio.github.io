# Publishing Guide

> For environment setup and local development, see [README.md](README.md).  
> All commands below require the **venv to be active** (see [Prerequisites](README.md#prerequisites)).

## Overview

This project generates the [Conio SDK documentation site](https://sdk-docs.conio.com) using MkDocs and publishes it to GitHub Pages via [`mike`](https://github.com/jimporter/mike), which supports multiple versions of the documentation living side by side.

The source files in this repository (`docs/`) always reflect the **latest version** of the SDK. Previous versions are not kept in source — they are preserved as separate subdirectories in the `gh-pages` branch, built and frozen at the time they were published. Users can switch between versions using the selector in the site header.

Each published version corresponds to a **breaking release of the SDK** and is identified by its version number (e.g. `2.5.0`). The alias `latest` always points to the most recently published version and is what users land on by default.

---

## When to publish a new version

Create a new documentation version whenever the SDK introduces **breaking changes**, i.e. changes that require existing integrations to be updated:

- Removed or renamed methods / classes / properties
- Changed method signatures (parameters added, removed, or reordered)
- Changed response types or error codes
- Behavioral changes that invalidate existing usage patterns

Do **not** create a new version for:
- Typo fixes or clarifications
- Documentation of new additive features (new methods that don't break existing ones)
- Formatting improvements

In those cases, [update the current version](#updating-an-existing-version) instead.

---

## Creating and previewing a new version locally

```sh
# Build and register the new version in the local gh-pages branch (no push)
mike deploy <version> latest --update-aliases

# Set it as the default landing version (first time only, or if changing default)
mike set-default latest

# Serve the versioned site locally at http://127.0.0.1:8000
mike serve
```

`mike serve` shows the full versioned site with the version selector, unlike `mkdocs serve` which shows only the current source. Verify the new version renders correctly and the selector lists all expected versions before publishing.

---

## Publishing a new version

```sh
# Deploy the new version to GitHub Pages and move the 'latest' alias to it
mike deploy --push --update-aliases <version> latest

# Tag the corresponding commit on main
git tag <version>
git push origin <version>
```

The tag should match the version string used with mike (e.g. `2.6.X` for `mike deploy ... 2.6.X latest`).

After pushing, verify the live site at https://sdk-docs.conio.com.

---

## Updating an existing version

Use this when adding documentation for new non-breaking features or fixing content in an already-published version without bumping the version number:

```sh
# Redeploy the same version, overwriting its content
mike deploy --push <version>
```

The `latest` alias is not moved — only the content of that version is updated.

---

## Useful maintenance commands

```sh
# List all published versions and their aliases
mike list

# Delete a version (e.g. a mistaken publish)
mike delete --push <version>

# Retitle a version label in the selector
mike retitle <version> "2.6.0 (LTS)"
```
