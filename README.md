# City Preference Voting (Static Build)

This directory contains the static assets deployed to GitHub Pages for the City Preference Voting app.

- `index.html` / `404.html`: SPA entry points generated via SvelteKit.
- `_app/`: hashed JS/CSS bundles produced via `npm run build`.
- `optimized-cities/`: 640px WebP thumbnails used by the voting UI.
- `favicon.png`: 1×1 placeholder to avoid 404s.

## Refresh workflow

```bash
cd /Users/romanchadnov/city_pruner/city-voting-svelte
node tools/build_city_manifest.mjs
BASE_PATH=golo-sovalka2026_1 npm run build
rsync -a --delete --exclude='.git/' build/ github-release/
cp github-release/index.html github-release/404.html
cd github-release
touch .nojekyll
```

Commit and push from inside `github-release/` once the bundle is refreshed.
