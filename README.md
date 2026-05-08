# atoue.io

Landing page for the [atoue](https://atoue.io) brand — a personal label for things Frans builds.

**Live:** [atoue.io](https://atoue.io)

## What it is

A static, hand-rolled site that lists shipped products, selected work, and what's currently brewing. Designed to grow as more projects slot into the existing sections.

## Pages

- `/` — landing
- `/resume.html` — resume with PDF download

## Stack

Static HTML/CSS, no build step. Hosted on [Cloudflare Pages](https://pages.cloudflare.com/), domain managed via Cloudflare.

## Structure

```
atoue.io/
├── index.html        landing page
├── resume.html       resume page
├── css/
│   ├── shared.css    shared base (typography, grain overlay, fade-in)
│   ├── landing.css   landing-specific
│   └── resume.css    resume-specific
└── assets/
    ├── favicon.svg
    └── Fransiskus-Budi-Resume.pdf
```

## Develop locally

No build step. Open `index.html` directly, or serve with any static server:

```bash
python -m http.server 8000
```

Drafts can be staged in `preview.html` (gitignored) before promoting to `index.html`.

## Featured products

- [taliu](https://taliu.atoue.io) — AI agent that knows Frans's work · [repo](https://github.com/fransiskusbudi/taliu)
