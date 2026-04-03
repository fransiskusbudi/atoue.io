# Resume Page & Project Restructure — Design Spec

## Overview

Add a styled resume page to atoue.io and restructure the project directory from a single-file site into an organized static site.

## Goals

1. Add a resume page (`resume.html`) with all content from Fransiskus's PDF resume, plus a personal intro and PDF download option.
2. Restructure the project directory into `css/`, `assets/` folders with shared and page-specific stylesheets.
3. Keep the landing page minimal — no nav bar, just add a "resume" link.
4. Update `.gitignore` to cover the new structure.

## Directory Structure

```
atoue.io/
├── index.html              # Landing page (refactored — styles extracted)
├── resume.html             # Resume page (new)
├── css/
│   ├── shared.css          # Shared styles: reset, fonts, grain overlay, variables
│   ├── landing.css         # Landing page-specific styles (includes overflow: hidden)
│   └── resume.css          # Resume page-specific styles
├── assets/
│   └── resume.pdf          # Downloadable PDF (user-supplied)
├── .gitignore
└── README.md
```

## Landing Page Changes

- Extract inline `<style>` block into `css/shared.css` (fonts, reset, grain, body — **not** `overflow: hidden`) and `css/landing.css` (container, logo, tagline, status, links, animations, `overflow: hidden` on body).
- Both `index.html` and `resume.html` must include the Google Fonts `<link>` tag in `<head>`.
- Add a "resume" link to the existing `.links` row (alongside github, twitter, contact).
- No other visual changes — the page stays as-is.

## Resume Page Design

### Approach

Single-column scroll layout. Pure HTML/CSS, no JavaScript required.

### Layout (top to bottom)

**Top Navigation:**
- Left: back link (`← atoue.io`) linking to `index.html`
- Right: "download pdf" button linking to `assets/resume.pdf`
- Separated from content by a subtle border

**Intro Section:**
- Name: "fransiskus budi" in DM Mono with gradient style (matching landing logo)
- Subtitle: "Edinburgh, UK · AI Engineer" in DM Mono, muted color
- Summary (first person):
  > I build data and AI systems from the ground up — from architecting data infrastructure to deploying AI-powered products. Over the past five years, I've worked across business intelligence, analytics, and AI engineering in both Indonesia and the United Kingdom, often as the person turning a blank slate into a working system. I'm drawn to the space where technical problems meet business decisions, and I care about building things that actually work, not just things that look impressive.
- Contact links row (monospace, muted, hover to white):
  - email: mailto:hi@atoue.io
  - linkedin: https://linkedin.com/in/fransiskusbudi/
  - github: https://github.com/fransiskusbudi

**Work Experience Section:**
- Section header: uppercase monospace "work experience" with bottom border
- 5 roles, each showing:
  - Role title (bold, white) + date range (monospace, muted) — flex row
  - Company + location (monospace, muted)
  - Bullet points (light gray, dot prefix) — transcribe all bullet points from the user's PDF resume exactly
- Roles in reverse chronological order (newest first):
  1. AI Engineer — Brainzyme (Aug 2025 – Present)
  2. Business Intelligence Lead — Jet Commerce Indonesia (Jul 2023 – Jul 2024)
  3. Business Intelligence Senior Associate — Lazada Indonesia (Nov 2022 – Jun 2023)
  4. Business Intelligence Associate — Shopee Indonesia (Oct 2021 – Nov 2022)
  5. Maintenance Analysis Engineer — Chandra Asri Group (Oct 2019 – Oct 2021)

Note: All work experience bullet points are already captured in the approved mockup at `.superpowers/brainstorm/97365-1775254416/resume-full-mockup.html`.

**Education Section:**
- Section header: uppercase monospace "education"
- Two entries: degree (bold) + institution on left, years on right
  - M.Sc. Data Science — The University of Edinburgh (2024–2025)
  - B.Eng. Chemical Engineering — Institut Teknologi Sepuluh Nopember (2015–2019)

**Technologies Section:**
- Section header: uppercase monospace "technologies"
- Three categories with labels:
  - Languages: Python, SQL, Scala, R, JavaScript
  - Technologies: PyTorch, scikit-learn, OpenCV, BigQuery, Postgres, Tableau, Power BI, Looker Studio, Vertex AI, GCP, n8n, APIs
  - Other: Generative AI, LLMs, RAG, LangChain, LangGraph, ETL, Data Modeling, A/B Testing, Web Scraping
- Each skill as a pill/tag (dark background, monospace, muted text)

### Visual Style

- Background: `#0a0a0a` (matching landing)
- Grain overlay (same SVG as landing)
- Fonts: DM Mono (headings, labels, nav) + Sora (body text)
- Name gradient: `linear-gradient(135deg, #e8e8e8 0%, #888 100%)`
- Max-width container: 700px, centered
- Fade-up animation on load (matching landing)
- Page `<title>`: "resume — atoue"
- Responsive: stacks flex rows on mobile (<600px) — applies to: role header (title + date), education entries (degree + year), top nav (back link + download), contact links

## Resume PDF

The user will supply `assets/resume.pdf` before deployment. During implementation, create the `assets/` directory and note the file is expected there.

## .gitignore Update

Add to existing `.gitignore`:
```
# Superpowers brainstorming
.superpowers/
```

## Tracked Directories

- `docs/` — committed to git (design specs are part of the project history)
- `.superpowers/` — git-ignored (brainstorming artifacts, ephemeral)

## What's NOT in Scope

- No build tools (Vite, webpack, etc.)
- No JavaScript interactivity on the resume page
- No nav bar on the landing page
- No changes to the landing page visual design (beyond extracting styles and adding resume link)
- No new fonts or color palette changes
