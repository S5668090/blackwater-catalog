# Blackwater Launcher catalog

Public data source for Blackwater Launcher. The launcher reads this file anonymously over HTTPS:

`https://raw.githubusercontent.com/S5668090/blackwater-catalog/refs/heads/main/catalog.json`

## Editing the catalog

Edit `catalog.json` on branch `main`, then commit the change. Launchers fetch the latest valid catalog at startup; users do not need a new EXE for game, DLC, cover, description, or download-link changes.

## Schema v1

Top-level:
- `schema_version`: must be integer `1`
- `catalog_version`: human-readable version
- `updated_at`: date string
- `games`: array of game entries

Each game:
- `id`: stable unique ID (ASCII letters, digits, hyphen, underscore)
- `name`: display name
- `steam_app_id`: positive integer
- `steam_folder`: exact folder name under Steam's `steamapps/common`
- `cover_url`: optional HTTPS cover image URL
- `featured`: true for large home tiles (currently CK3 and HOI4)
- `dlcs`: array (may be empty)

Each DLC:
- `id`: unique within its game
- `name`: display name
- `description`: short description
- `download_url`: HTTPS ZIP URL; empty string disables install until supplied
- `featured`: true for a highlighted DLC card

The launcher rejects invalid JSON, duplicate IDs/AppIDs, non-HTTPS URLs, unsafe Steam folder names, unknown schema versions, empty game arrays, and catalogs above its size/count limits.

## Security

This repository is public. Never commit Personal Access Tokens, passwords, private links, or other secrets. The launcher only needs anonymous read access; write credentials belong only in a trusted local admin workflow or GitHub's secret storage. If a token has been exposed, revoke it immediately.

## Important

The current entries include placeholder DLC labels. Replace those with accurate DLC metadata and trusted archive URLs before treating them as published downloads.

## Admin panel

A separate browser-based admin panel is available in [`admin/`](admin/). To publish it as a website, enable GitHub Pages in **Settings → Pages**, select branch `main` and folder `/ (root)`. The panel will then be available at:

`https://s5668090.github.io/blackwater-catalog/admin/`

See [`admin/README.md`](admin/README.md) for token permissions and security instructions. The panel requests a narrowly scoped Fine-grained token at runtime and does not save it in the page or repository.
