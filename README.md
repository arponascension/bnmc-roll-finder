# BNMC Roll Finder — GitHub Pages

A React/Vite site where a student enters a BNMC roll number and gets the assigned centre, building/position, floor and room/hall.

The data is generated at build time from the official BNMC PDF:

https://objectstorage.ap-dcc-gazipur-1.oraclecloud15.com/n/axvjbnqprylg/b/V2Ministry/o/office-bnmc/2026/8/20427cd0-ee2f-46bf-977b-035444407762.pdf

## Run locally

```bash
npm install
npm run build
npm run dev
```

## Deploy to GitHub Pages

1. Create a GitHub repository, e.g. `bnmc-roll-finder`.
2. Upload this project.
3. In GitHub: **Settings → Pages → Source: GitHub Actions**.
4. Use the workflow below as `.github/workflows/deploy.yml`.

```yaml
name: Deploy
on:
  push:
    branches: [main]
permissions:
  contents: read
  pages: write
  id-token: write
jobs:
  deploy:
    runs-on: ubuntu-latest
    environment:
      name: github-pages
    steps:
      - uses: actions/checkout@v4
      - uses: actions/setup-node@v4
        with:
          node-version: 20
      - run: npm install
      - run: npm run build
      - uses: actions/configure-pages@v5
      - uses: actions/upload-pages-artifact@v3
        with:
          path: ./dist
      - uses: actions/deploy-pages@v4
```

> Note: the parser depends on the PDF's current table/text structure. Always verify a few roll numbers against the official PDF before publishing a high-stakes exam utility.
