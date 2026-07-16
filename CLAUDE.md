# CLAUDE.md

## What this repo is

Static marketing/docs site for **HeadyAI**, served at **https://heady-ai.com** via GitHub Pages (the `CNAME` file holds the custom domain). Plain hand-written HTML/CSS/JS — no framework, no build step, no package manager, no CI workflows (`.github/` does not exist). What is committed at the repo root is exactly what gets served.

The site presents "The Science Behind HeadyOS" — Continuous Semantic Logic (CSL), Vector Symbolic Architecture, Sacred Geometry topology, and the HeadySystems patent portfolio — and cross-links the wider Heady ecosystem (headysystems.com, headyme.com, headyos.com, headyconnection.org/.com, headyex.com, etc.).

## Layout

| Path | Purpose |
|------|---------|
| `index.html` | Landing page (~600 lines). Single-page layout with anchor-nav sections (`#research`, `#patents`, `#nodes`, `#features`, `#faq`, ...). Styling = `/shared/css/heady-base.css` plus a page-specific `<style>` block that sets the purple accent (`#8b5cf6`). |
| `docs/index.html` | Docs page (CSL Engine, Sacred Geometry, VSA). **Fully self-contained** — all CSS inline; it does not use `shared/`. |
| `shared/css/heady-base.css` | "Heady Design System — Dark Glass Premium": phi-scaled spacing/type variables, glass surfaces, shared across the 9 Heady domains. |
| `shared/js/heady-sacred-geometry.js` | Stub defining `window.HeadySacredGeometry` (console-log `init` only). |
| `shared/js/heady-shared.js` | Stub defining `window.HeadyShared` (console-log `init` only). |
| `CNAME` | `heady-ai.com` — required for GitHub Pages custom domain; do not remove. |
| `robots.txt` | Allows all crawlers; points to `https://heady-ai.com/sitemap.xml`. |
| `sitemap.xml` | Lists `/`, `/experiments`, `/products`. Note: `/experiments` and `/products` currently have no corresponding files in the repo. |

## Runtime integrations in index.html

- **Sentry** browser SDK loaded from `browser.sentry-cdn.com` with a hardcoded public DSN, `environment: "production"`, `tracesSampleRate: 0.2`.
- **Site globals**: `window.__HEADY_SITE_META__` (`slug: "heady-ai"`, `domain: "heady-ai.com"`, accent, sacred-geometry motif) and `window.__HEADY_AUTH_CONFIG__` pointing at `https://auth.headysystems.com` session/provider endpoints.
- **Auth widget** (`#heady-auth-widget`) posts to the auth endpoints above with `credentials: 'include'`.
- **HeadyBuddy chat FAB**: self-contained IIFE at the bottom of `index.html` that builds a floating chat button/panel via DOM APIs and POSTs to `https://manager.headysystems.com/api/buddy/chat`. Per HEA-231, hover effects use CSS `:hover` — do **not** reintroduce inline `onmouseover`/`onmouseout` handlers inside `innerHTML` strings (they caused a production SyntaxError and violate CSP).
- **Google Fonts** (Space Grotesk + Inter on the landing page; Inter + JetBrains Mono on the docs page).

## Conventions

- **Canonical domain is `heady-ai.com`** (hyphenated). `headyai.com` was a bug fixed in commit 95bffdf — never reintroduce it in links, meta tags, or JSON-LD.
- Shared assets are referenced with absolute root paths (`/shared/css/heady-base.css`, `/shared/js/...`), which is what GitHub Pages serves at the domain root.
- Design tokens are phi-based (`--phi: 1.618...`, Fibonacci pixel steps in the docs page). Reuse the existing CSS custom properties rather than adding raw values.
- SEO surfaces travel together: when adding or removing a page, update `sitemap.xml` (and `lastmod`), and keep the canonical `<link>`, Open Graph tags, and JSON-LD blocks consistent with `heady-ai.com`.
- `docs/index.html` intentionally carries its own inline styles; keep it self-contained rather than coupling it to `shared/`.

## Editing / testing

There is nothing to build or install. Edit the HTML/CSS/JS directly and verify by opening the files in a browser or serving the repo root with any static file server (root-absolute `/shared/...` paths require serving from the repo root, not opening via `file://`). Deployment happens automatically when changes land on the default branch GitHub Pages publishes from.
