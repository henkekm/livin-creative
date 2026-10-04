# Livin' Creative

Static website for [livincreative.art](https://livincreative.art), hosted on Porkbun cPanel (Apache/LiteSpeed).

## Project layout

| Path | Purpose |
| --- | --- |
| `index.html`, `favicon.svg` | Site entry point |
| `styles/`, `scripts/` | CSS and JavaScript |
| `_images/`, `_collateral/` | Images, logos and fonts |
| `events-library/` | Event JSON files + `manifest.json` |
| `kits-library/` | Kit JSON files + `manifest.json` |
| `.htaccess` | Server config: HTTPS redirect, caching, compression, MIME types, security headers |
| `.cpanel.yml` | cPanel Git™ Version Control deployment tasks |

The site fetches its data from root-relative paths (`/events-library/…`, `/kits-library/…`), so it must be served from the **root of the domain** (`public_html` for the primary domain).

## Deploying to cPanel

### Option A — cPanel Git™ Version Control (recommended)

1. In cPanel, open **Git™ Version Control** → **Create**.
2. Enable **Clone a Repository**, enter this repository's clone URL, and choose a repository path outside `public_html` (e.g. `repositories/livin-creative`).
   For a private repository, add an SSH key in cPanel (**SSH Access**) and register it as a deploy key on GitHub.
3. After cloning, open **Manage** → **Pull or Deploy**, click **Update from Remote**, then **Deploy HEAD Commit**.
   `.cpanel.yml` copies the site files into `~/public_html/`.
4. Repeat step 3 whenever new changes are pushed to GitHub.

### Option B — File Manager / FTP upload

Upload the following into `public_html` (keep the folder structure):

```
index.html  favicon.svg  .htaccess
styles/  scripts/  _images/  _collateral/  events-library/  kits-library/
```

`.htaccess` is a hidden file — in File Manager enable **Settings → Show Hidden Files (dotfiles)** to see it.

### DNS and SSL

1. In Porkbun, point `livincreative.art` (and `www`) at the cPanel hosting (remove the old GitHub Pages `A`/`CNAME` records).
2. In cPanel, run **SSL/TLS Status → Run AutoSSL** once DNS has propagated. `.htaccess` then redirects all traffic to `https://livincreative.art`.
3. Remove the custom domain from the repository's GitHub Pages settings and disable Pages.

## Adding events and kits

Copy the template in `events-library/_template/` or `kits-library/_template/`, fill it in, and add its path to the corresponding `manifest.json` with `"active": true`. Images go in `_images/workshops/` or `_images/kits/`. Redeploy afterwards.
