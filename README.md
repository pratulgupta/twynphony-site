# twynphony.org (mirror)

Static mirror of [twynphony.org](https://twynphony.org), ready for GitHub Pages deployment.

## Structure

- `index.html` and 20 other top-level `.html` pages — full site content
- `isteam/`, `blobby/`, `ceph-p3-01/`, `signals/`, `gfonts/` — asset directories from the GoDaddy CDN (`img1.wsimg.com`)
- `manifest.webmanifest`, `robots.txt` — site metadata
- `.nojekyll` — disables GitHub Pages' Jekyll processing (required because some paths contain `_` and `:`)

## Deploy to GitHub Pages

```bash
git init
git add -A
git commit -m "Initial mirror of twynphony.org"
git branch -M main
gh repo create twynphony-site --public --source . --push
gh api -X POST repos/:owner/twynphony-site/pages -f source[branch]=main -f source[path]=/
```

After ~1 minute, the site will be live at `https://<owner>.github.io/twynphony-site/`.

## Notes

- All asset references have been rewritten from CDN URLs (`//img1.wsimg.com/...`) to relative paths, so the site is self-contained.
- File names contain `:` characters (valid on macOS/Linux/GitHub Pages, but **will fail to checkout on Windows**).
- External embeds (YouTube, Vimeo, Facebook) still load from their original hosts — only same-host assets are mirrored.
- Size: ~307 MB (largely responsive image variants; each photo has 10+ pixel-width versions for srcset).
