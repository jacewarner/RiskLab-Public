# RiskLab

This repository hosts the RiskLab documentation site built with
[Docusaurus](https://docusaurus.io/). It is optimized for quantitative research:
MDX pages can mix prose, KaTeX-rendered math, and embedded React calculators so
authors never have to link out to external tools.

## Getting started

Prerequisites:

- Node.js 20+ (`.nvmrc` pins to 20.19.5; `nvm use`, `volta install node@20`, etc.)

```bash
npm install
npm run start
```

- The dev server runs on http://localhost:3000/ and hot-reloads as you edit files
  in `docs/` or `src/`.
- Open the repository in VS Code to edit Markdown/MDX pages and React components
  side by side.

## Containerized workflows

- Suggested port: 8090 (less common than 3000/8080; run `docker ps` to ensure
  it is free, or set `PORT=####` below).
- Dev (hot reload): `docker build -f Dockerfile.dev -t risklab-dev .` then
  `docker run --rm -it -p 8090:3000 -e PORT=3000 -e HOST=0.0.0.0 -v "$PWD":/app -v /app/node_modules risklab-dev`
  (mount the repo for live edits; change 8090 if you prefer).
- Prod (static assets baked in): `docker build -t risklab .` then
  `docker run --rm -p 8090:3000 -e PORT=3000 risklab`
  (serves the `build/` output via `serve`).
- Docker Compose (familiar UX): `PORT=8090 docker compose up dev` for hot reload
  or `PORT=8090 docker compose up prod` for the built site; edit PORT to any free
  host port.
- Make targets: `make build-dev` or `make build-prod` (defaults to PORT=8090,
  uses `docker compose down` then `up` for the chosen service).
- Cloudflare Tunnel example: point the tunnel at the mapped port,
  e.g. `cloudflared tunnel --url http://localhost:8090`.

## Authoring features

- `remark-math` and `rehype-katex` are preconfigured, so wrap formulas in single
  `$...$` or double `$$...$$` fences.
- Reusable interactive widgets live in `src/components/`. See
  `src/components/Black76Calculator.tsx` + `docs/options/black76.mdx` or
  `src/components/SpreadKirkCalculator.tsx` + `docs/options/spread-kirk.mdx`
  for end-to-end templates.
- Use whatever React tooling you prefer (hooks, context, charts) as long as it
  can execute client-side.

## Production build

```bash
npm run build
npm run serve   # optional sanity-check of the static build
```

The static output lands in `build/` and can be deployed behind any HTTP server or
container image that can serve static assets.
