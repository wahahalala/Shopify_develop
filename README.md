# Shopify Develop — Dawn Theme Learning Repository

English | [中文](./README.zh-CN.md)

This repository is cloned from Shopify's official open-source theme **Dawn 16.1.1** (`main` branch) for local study and secondary development practice.

> The original theme is copyrighted by Shopify Inc.; see [LICENSE.md](./LICENSE.md) for the license. This repo is for personal learning only. If you later submit a modified theme to the Theme Store, it must meet official requirements such as being substantially different from Dawn.

## Repository Background

- **Baseline version**: Dawn 16.1.1 (commit `3e9ee228`)
- **Remote configuration**:

  | Remote | URL | Purpose |
  | --- | --- | --- |
  | `origin` | `https://github.com/wahahalala/Shopify_develop.git` | Personal repository; used for daily push / pull |
  | `upstream` | `https://github.com/Shopify/dawn.git` | Official Shopify upstream; used to track official updates |

## Directory Structure

Dawn is an Online Store 2.0 theme that follows the standard Shopify theme directory conventions:

| Directory / File | Purpose |
| --- | --- |
| `layout/` | Global layout templates (e.g. `theme.liquid` site skeleton, `password.liquid` password page) |
| `templates/` | Page entry templates, mostly JSON templates such as `index.json`, `product.json`, `collection.json`, `cart.json`, `search.json` |
| `sections/` | Page sections that can be referenced, reused, and reordered within templates (48 files) |
| `snippets/` | Reusable Liquid code snippets (39 files) |
| `assets/` | Static assets: CSS, JavaScript, images, SVG, etc. (191 files) |
| `config/` | Theme settings definition (`settings_schema.json`) and default settings data (`settings_data.json`) |
| `locales/` | Translation files (`.json`) and their schemas for multiple languages |
| `.github/workflows/` | GitHub Actions: Theme Check, Lighthouse, and CLA checks |
| `.theme-check.yml` | Theme Check static-analysis rule toggles |
| `release-notes.md` | Release notes for each version |

## Local Development

### Prerequisites

- Install the [Shopify CLI](https://github.com/Shopify/shopify-cli) (Node.js environment)
- A Shopify development store you can use for development

### Common Commands

```bash
# Start the local dev server and preview theme changes live
shopify theme dev

# Push the local theme to a store
shopify theme push

# Run Theme Check static analysis
shopify theme check
```

### Code Standards

- Formatter: Prettier (config in `.prettierrc.json`)
- Linter: Theme Check, with rule toggles in `.theme-check.yml`

## Syncing Upstream Updates

When you need to merge the latest changes from the official Shopify Dawn repository:

```bash
# 1. Fetch the latest code from upstream
git fetch upstream

# 2. Merge upstream/main into your current local branch
git merge upstream/main

# 3. Resolve conflicts, then push to your personal repository
git push origin main
```

## Committing and Pushing

```bash
# Check status
git status

# Stage changes and commit
git add .
git commit -m "commit message"

# Push to your personal repository (origin/main is already tracked)
git push
```

## CI and Secrets

The Lighthouse workflow in `.github/workflows/ci.yml` reads store URL, access token, and other settings from GitHub Secrets (e.g. `SHOP_STORE_OS2`, `SHOP_ACCESS_TOKEN`, `LHCI_GITHUB_TOKEN`). These sensitive values are **not written into repository files**. To enable the corresponding workflows in this personal repository, configure the same Secrets yourself under **Settings → Secrets and variables → Actions**.

## Security Notes

- This repository contains no plaintext sensitive information such as `.env` files, private keys, certificates, hardcoded tokens, or store domains.
- Local Git credentials are stored by the system credential manager. Never commit or write a Personal Access Token into the repository.
