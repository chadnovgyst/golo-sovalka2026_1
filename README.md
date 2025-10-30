# City Preference Voting (Static Build)

This directory contains the static assets deployed to GitHub Pages for the City Preference Voting app.

- `index.html` / `404.html`: SPA entry points generated via SvelteKit.
- `_app/`: hashed JS/CSS bundles produced by `npm run build`.
- `optimized-cities/`: 640px WebP thumbnails used by the voting UI.

## Refreshing the bundle

```bash
cd /Users/romanchadnov/city_pruner/city-voting-svelte
python3 tools/build_thumbnails.py
node tools/build_city_manifest.mjs
BASE_PATH=golo-sovalka2026_1 npm run build
rsync -a --delete --exclude='.git/' build/ github-release/
cp github-release/index.html github-release/404.html
cd github-release
touch .nojekyll
git add .
git commit -m "build: update static bundle"
```

The source city metadata now lives under `data/cities/` and only optimised thumbnails are shipped.
