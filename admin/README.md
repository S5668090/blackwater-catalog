# Blackwater Admin Panel

Separate browser-based admin UI for editing `catalog.json`. It is not part of the Windows launcher.

## Publish with GitHub Pages

1. Open **Settings → Pages** in this repository.
2. Under **Build and deployment**, choose **Deploy from a branch**.
3. Select branch `main` and folder `/ (root)`, then save.
4. After GitHub finishes publishing, open:

   `https://s5668090.github.io/blackwater-catalog/admin/`

The page source is `admin/index.html`.

## Create the access token

Create a **Fine-grained personal access token** in your GitHub settings:

- Resource owner: `S5668090`
- Repository access: **Only select repositories** → `blackwater-catalog`
- Repository permissions:
  - **Contents: Read and write**
  - **Metadata: Read-only** (usually granted automatically)
- Set an expiration date.

Paste the token into the panel when connecting. The panel keeps it only in JavaScript memory for that open tab; it does not write it to localStorage/sessionStorage, the repository, catalog, or launcher. It sends requests directly to `api.github.com` over HTTPS.

Do not paste tokens into chat, commit them to Git, or put them into the launcher. If a token is exposed, revoke it immediately.

## Current features

- Load the current catalog from `main`
- Add, edit, and delete games
- Add, edit, and delete DLC entries
- Edit Steam AppID, Steam folder, cover URL, DLC description and archive URL
- Validate IDs, duplicate IDs/AppIDs, Steam folder names, and HTTPS URLs
- Publish the updated JSON as one commit to `main`

Images and ZIP archives are currently referenced by HTTPS URL; the first version does not upload binary files. Put files on a trusted HTTPS host and paste their URLs into the relevant fields.

## Important

The GitHub Pages site itself is public because the repository is public. The panel does not provide a separate login service; write access is gated by the Fine-grained token that the administrator enters. Use a narrowly scoped, expiring token and do not use an all-repositories token.
