# City Preference Voting (Static Build)

This directory contains the static assets deployed to GitHub Pages for the City Preference Voting app.

- `index.html` / `404.html`: SPA entry point generated via SvelteKit.
- `_app/`: hashed JS/CSS bundles produced by `npm run build`.
- `cities/`: per-city metadata (`data.js`) without full-resolution images.
- `optimized-cities/`: 640px WebP thumbnails used by the voting UI.

To refresh the bundle locally:

```bash
cd ..
python3 tools/build_thumbnails.py
node tools/build_city_manifest.mjs
BASE_PATH=golo-sovalka2026_1 npm run build
find build/cities -type d -name images -exec rm -rf {} +
rsync -a --delete --exclude='.git/' build/ github-release/
cp github-release/index.html github-release/404.html
touch github-release/.nojekyll
```

Commit and push the updated contents from inside this folder.
