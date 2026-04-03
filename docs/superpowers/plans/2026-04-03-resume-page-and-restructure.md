# Resume Page & Project Restructure — Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Add a resume page to atoue.io and restructure the project from a single-file site into organized `css/` and `assets/` folders with shared and page-specific stylesheets.

**Architecture:** Extract inline styles from `index.html` into `css/shared.css` and `css/landing.css`. Create a new `resume.html` that uses `css/shared.css` + `css/resume.css`. All content is static HTML/CSS — no build tools or JS.

**Tech Stack:** HTML, CSS, Google Fonts (DM Mono, Sora)

**Spec:** `docs/superpowers/specs/2026-04-03-resume-page-and-restructure-design.md`

**Approved mockup:** `.superpowers/brainstorm/97365-1775254416/resume-full-mockup.html`

---

## File Map

| Action | File | Responsibility |
|--------|------|----------------|
| Create | `css/shared.css` | Reset, body base styles, grain overlay, fonts, fadeUp animation. **Not** `overflow: hidden`. |
| Create | `css/landing.css` | Landing page layout: container centering, logo, tagline, status, links, `overflow: hidden` on body. |
| Create | `css/resume.css` | Resume page layout: top-nav, intro, roles, education, tech pills, responsive breakpoints. |
| Modify | `index.html` | Remove inline `<style>`, link to `css/shared.css` + `css/landing.css`, add "resume" link. |
| Create | `resume.html` | Full resume page linking to `css/shared.css` + `css/resume.css`. |
| Create | `assets/` | Directory for resume PDF (user-supplied later). |
| Modify | `.gitignore` | Add `.superpowers/` entry. |

---

### Task 1: Create `css/shared.css`

Extract the shared styles from `index.html` inline `<style>` block.

**Files:**
- Create: `css/shared.css`

- [ ] **Step 1: Create the `css/` directory and `shared.css`**

```css
/* shared.css — common styles across all pages */
* { margin: 0; padding: 0; box-sizing: border-box; }

body {
    background: #0a0a0a;
    color: #e8e8e8;
    font-family: 'Sora', sans-serif;
    min-height: 100vh;
}

.grain {
    position: fixed;
    top: -50%; left: -50%;
    width: 200%; height: 200%;
    background-image: url("data:image/svg+xml,%3Csvg viewBox='0 0 256 256' xmlns='http://www.w3.org/2000/svg'%3E%3Cfilter id='n'%3E%3CfeTurbulence type='fractalNoise' baseFrequency='0.9' numOctaves='4' stitchTiles='stitch'/%3E%3C/filter%3E%3Crect width='100%25' height='100%25' filter='url(%23n)' opacity='0.04'/%3E%3C/svg%3E");
    pointer-events: none;
    z-index: 100;
}

@keyframes fadeUp {
    0% { opacity: 0; transform: translateY(20px); }
    100% { opacity: 1; transform: translateY(0); }
}
```

Note: `overflow: hidden` is intentionally excluded — it would break scrolling on the resume page. It belongs in `landing.css`.

- [ ] **Step 2: Commit**

```bash
git add css/shared.css
git commit -m "feat: create shared.css with base styles extracted from index.html"
```

---

### Task 2: Create `css/landing.css`

Extract landing-page-specific styles from `index.html`.

**Files:**
- Create: `css/landing.css`

- [ ] **Step 1: Create `landing.css`**

```css
/* landing.css — landing page specific styles */
body {
    display: flex;
    align-items: center;
    justify-content: center;
    overflow: hidden;
}

.container {
    text-align: center;
    animation: fadeUp 1.2s ease-out;
}

.logo {
    font-family: 'DM Mono', monospace;
    font-weight: 300;
    font-size: clamp(3rem, 8vw, 6rem);
    letter-spacing: 0.3em;
    text-transform: lowercase;
    margin-bottom: 1.5rem;
    background: linear-gradient(135deg, #e8e8e8 0%, #888 100%);
    -webkit-background-clip: text;
    -webkit-text-fill-color: transparent;
    background-clip: text;
}

.tagline {
    font-weight: 300;
    font-size: clamp(0.85rem, 2vw, 1.05rem);
    color: #555;
    letter-spacing: 0.15em;
    text-transform: lowercase;
    margin-bottom: 3rem;
}

.status {
    display: inline-flex;
    align-items: center;
    gap: 0.6rem;
    font-family: 'DM Mono', monospace;
    font-size: 0.75rem;
    color: #444;
    letter-spacing: 0.08em;
}

.dot {
    width: 6px;
    height: 6px;
    background: #2ecc71;
    border-radius: 50%;
    animation: pulse 2s ease-in-out infinite;
}

.links {
    margin-top: 2.5rem;
    display: flex;
    gap: 2rem;
    justify-content: center;
}

.links a {
    font-family: 'DM Mono', monospace;
    font-size: 0.8rem;
    color: #555;
    text-decoration: none;
    letter-spacing: 0.05em;
    transition: color 0.3s ease;
}

.links a:hover {
    color: #e8e8e8;
}

@keyframes pulse {
    0%, 100% { opacity: 0.4; }
    50% { opacity: 1; }
}
```

- [ ] **Step 2: Commit**

```bash
git add css/landing.css
git commit -m "feat: create landing.css with landing page styles"
```

---

### Task 3: Refactor `index.html`

Remove inline styles, link external CSS files, add resume link.

**Files:**
- Modify: `index.html`

- [ ] **Step 1: Replace `index.html` contents**

Replace the entire file with:

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>atoue</title>
    <link rel="preconnect" href="https://fonts.googleapis.com">
    <link href="https://fonts.googleapis.com/css2?family=DM+Mono:wght@300;400&family=Sora:wght@300;400;600&display=swap" rel="stylesheet">
    <link rel="stylesheet" href="css/shared.css">
    <link rel="stylesheet" href="css/landing.css">
</head>
<body>
    <div class="grain"></div>
    <div class="container">
        <div class="logo">atoue</div>
        <p class="tagline">something is brewing</p>
        <div class="status">
            <span class="dot"></span>
            <span>building in progress</span>
        </div>
        <div class="links">
            <a href="resume.html">resume</a>
            <a href="https://github.com/fransiskusbudi" target="_blank">github</a>
            <a href="https://x.com/atouexyz" target="_blank">twitter</a>
            <a href="mailto:hi@atoue.io">contact</a>
        </div>
    </div>
</body>
</html>
```

- [ ] **Step 2: Open `index.html` in browser and verify it looks identical to original**

```bash
open index.html
```

Verify: dark background, centered logo with gradient, tagline, pulsing dot, four links (resume, github, twitter, contact). No visual difference except the new "resume" link.

- [ ] **Step 3: Commit**

```bash
git add index.html
git commit -m "refactor: extract inline styles to external CSS, add resume link"
```

---

### Task 4: Create `css/resume.css`

All resume-page-specific styles. Reference the approved mockup for exact values.

**Files:**
- Create: `css/resume.css`

- [ ] **Step 1: Create `resume.css`**

```css
/* resume.css — resume page specific styles */
body {
    line-height: 1.6;
}

.container {
    max-width: 700px;
    margin: 0 auto;
    padding: 3rem 1.5rem 5rem;
    animation: fadeUp 1.2s ease-out;
}

/* Top nav */
.top-nav {
    display: flex;
    justify-content: space-between;
    align-items: center;
    margin-bottom: 3rem;
    padding-bottom: 1rem;
    border-bottom: 1px solid #1a1a1a;
}

.top-nav a {
    font-family: 'DM Mono', monospace;
    font-size: 0.8rem;
    color: #555;
    text-decoration: none;
    letter-spacing: 0.05em;
    transition: color 0.3s ease;
}

.top-nav a:hover { color: #e8e8e8; }

.download-btn {
    display: inline-flex;
    align-items: center;
    gap: 0.4rem;
    background: #151515;
    border: 1px solid #222;
    padding: 0.4rem 1rem;
    border-radius: 4px;
    font-family: 'DM Mono', monospace;
    font-size: 0.75rem;
    color: #888;
    text-decoration: none;
    transition: all 0.3s ease;
}

.download-btn:hover {
    color: #e8e8e8;
    border-color: #444;
}

/* Intro */
.intro { margin-bottom: 3rem; }

.intro .name {
    font-family: 'DM Mono', monospace;
    font-weight: 300;
    font-size: clamp(1.8rem, 4vw, 2.4rem);
    letter-spacing: 0.1em;
    background: linear-gradient(135deg, #e8e8e8 0%, #888 100%);
    -webkit-background-clip: text;
    -webkit-text-fill-color: transparent;
    background-clip: text;
    margin-bottom: 0.5rem;
}

.intro .subtitle {
    font-family: 'DM Mono', monospace;
    font-size: 0.8rem;
    color: #555;
    letter-spacing: 0.08em;
    margin-bottom: 1.2rem;
}

.intro .summary {
    font-size: 0.9rem;
    font-weight: 300;
    color: #888;
    line-height: 1.8;
    max-width: 600px;
}

.intro .contact-links {
    margin-top: 1rem;
    display: flex;
    gap: 1.5rem;
}

.intro .contact-links a {
    font-family: 'DM Mono', monospace;
    font-size: 0.75rem;
    color: #444;
    text-decoration: none;
    letter-spacing: 0.05em;
    transition: color 0.3s ease;
}

.intro .contact-links a:hover { color: #e8e8e8; }

/* Section headers */
.section-header {
    font-family: 'DM Mono', monospace;
    font-size: 0.75rem;
    color: #555;
    letter-spacing: 0.15em;
    text-transform: uppercase;
    margin-bottom: 1.5rem;
    padding-bottom: 0.5rem;
    border-bottom: 1px solid #1a1a1a;
}

section { margin-bottom: 3rem; }

/* Roles */
.role { margin-bottom: 2rem; }

.role-header {
    display: flex;
    justify-content: space-between;
    align-items: baseline;
    flex-wrap: wrap;
    gap: 0.5rem;
    margin-bottom: 0.2rem;
}

.role-title {
    font-weight: 600;
    font-size: 1rem;
    color: #e8e8e8;
}

.role-date {
    font-family: 'DM Mono', monospace;
    font-size: 0.75rem;
    color: #444;
}

.role-company {
    font-family: 'DM Mono', monospace;
    font-size: 0.8rem;
    color: #666;
    margin-bottom: 0.3rem;
}

.role ul {
    list-style: none;
    padding: 0;
}

.role li {
    font-size: 0.85rem;
    font-weight: 300;
    color: #888;
    line-height: 1.7;
    padding-left: 1rem;
    position: relative;
    margin-bottom: 0.3rem;
}

.role li::before {
    content: '·';
    position: absolute;
    left: 0;
    color: #444;
}

/* Education */
.edu-item {
    display: flex;
    justify-content: space-between;
    align-items: baseline;
    flex-wrap: wrap;
    gap: 0.5rem;
    margin-bottom: 0.8rem;
}

.edu-item .degree {
    font-size: 0.9rem;
    color: #ccc;
}

.edu-item .degree strong {
    color: #e8e8e8;
    font-weight: 600;
}

.edu-item .year {
    font-family: 'DM Mono', monospace;
    font-size: 0.75rem;
    color: #444;
}

/* Tech pills */
.tech-category {
    margin-bottom: 1rem;
}

.tech-label {
    font-family: 'DM Mono', monospace;
    font-size: 0.7rem;
    color: #555;
    letter-spacing: 0.08em;
    margin-bottom: 0.5rem;
}

.pills {
    display: flex;
    flex-wrap: wrap;
    gap: 0.4rem;
}

.pill {
    background: #151515;
    border: 1px solid #1a1a1a;
    color: #888;
    padding: 0.25rem 0.7rem;
    border-radius: 3px;
    font-family: 'DM Mono', monospace;
    font-size: 0.7rem;
    letter-spacing: 0.03em;
}

/* Responsive */
@media (max-width: 600px) {
    .role-header { flex-direction: column; gap: 0.1rem; }
    .edu-item { flex-direction: column; gap: 0.1rem; }
    .top-nav { flex-direction: column; gap: 0.8rem; align-items: flex-start; }
    .intro .contact-links { flex-direction: column; gap: 0.5rem; }
}
```

- [ ] **Step 2: Commit**

```bash
git add css/resume.css
git commit -m "feat: create resume.css with all resume page styles"
```

---

### Task 5: Create `resume.html`

The full resume page with all content from the approved mockup.

**Files:**
- Create: `resume.html`

- [ ] **Step 1: Create `resume.html`**

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>resume — atoue</title>
    <link rel="preconnect" href="https://fonts.googleapis.com">
    <link href="https://fonts.googleapis.com/css2?family=DM+Mono:wght@300;400&family=Sora:wght@300;400;600&display=swap" rel="stylesheet">
    <link rel="stylesheet" href="css/shared.css">
    <link rel="stylesheet" href="css/resume.css">
</head>
<body>
    <div class="grain"></div>
    <div class="container">
        <!-- Top Nav -->
        <nav class="top-nav">
            <a href="index.html">← atoue.io</a>
            <a href="assets/resume.pdf" class="download-btn" target="_blank">↓ download pdf</a>
        </nav>

        <!-- Intro -->
        <div class="intro">
            <div class="name">fransiskus budi</div>
            <div class="subtitle">Edinburgh, UK · AI Engineer</div>
            <p class="summary">
                I build data and AI systems from the ground up — from architecting data infrastructure to deploying AI-powered products. Over the past five years, I've worked across business intelligence, analytics, and AI engineering in both Indonesia and the United Kingdom, often as the person turning a blank slate into a working system. I'm drawn to the space where technical problems meet business decisions, and I care about building things that actually work, not just things that look impressive.
            </p>
            <div class="contact-links">
                <a href="mailto:hi@atoue.io">email</a>
                <a href="https://linkedin.com/in/fransiskusbudi/" target="_blank">linkedin</a>
                <a href="https://github.com/fransiskusbudi" target="_blank">github</a>
            </div>
        </div>

        <!-- Work Experience -->
        <section>
            <div class="section-header">work experience</div>

            <div class="role">
                <div class="role-header">
                    <span class="role-title">AI Engineer</span>
                    <span class="role-date">Aug 2025 – Present</span>
                </div>
                <div class="role-company">Brainzyme · Edinburgh, United Kingdom</div>
                <ul>
                    <li>Developed and deployed a multimodal AI customer support chatbot across web, WhatsApp, and email, improving response scalability and consistency using RAG.</li>
                    <li>Built an AI-powered audit layer to evaluate chatbot responses against internal guidelines and quality standards.</li>
                    <li>Built a zero-to-one AI content generation pipeline for image and video assets, integrating generative models, workflow automation, and scheduling.</li>
                    <li>Automated operational workflows, including order-processing support, to reduce manual effort and improve execution speed.</li>
                </ul>
            </div>

            <div class="role">
                <div class="role-header">
                    <span class="role-title">Business Intelligence Lead</span>
                    <span class="role-date">Jul 2023 – Jul 2024</span>
                </div>
                <div class="role-company">Jet Commerce Indonesia · Jakarta, Indonesia</div>
                <ul>
                    <li>Led a 5-person BI team in building the company's data architecture from 0 to 1, establishing a scalable foundation for analytics and reporting.</li>
                    <li>Built data collection workflows by developing web scraping and API-based pipelines using Selenium, BeautifulSoup, and Python.</li>
                    <li>Designed and optimized end-to-end ETL and dashboard workflows, improving reporting speed and visibility.</li>
                    <li>Partnered with cross-functional teams to translate data insights into actionable business strategies.</li>
                </ul>
            </div>

            <div class="role">
                <div class="role-header">
                    <span class="role-title">Business Intelligence Senior Associate</span>
                    <span class="role-date">Nov 2022 – Jun 2023</span>
                </div>
                <div class="role-company">Lazada Indonesia · Jakarta, Indonesia</div>
                <ul>
                    <li>Delivered decision-ready analysis to senior stakeholders to support strategic planning and performance management.</li>
                    <li>Automated recurring performance reporting using SQL and Python, improving efficiency and reducing manual work.</li>
                    <li>Built data pipelines for recurring business reporting, streamlining data extraction and improving reliability.</li>
                </ul>
            </div>

            <div class="role">
                <div class="role-header">
                    <span class="role-title">Business Intelligence Associate</span>
                    <span class="role-date">Oct 2021 – Nov 2022</span>
                </div>
                <div class="role-company">Shopee Indonesia · Jakarta, Indonesia</div>
                <ul>
                    <li>Built dashboards and data models to improve visibility into business operations and support faster decision-making.</li>
                    <li>Engineered an automated user-list generation for marketing campaigns, streamlining execution workflows.</li>
                    <li>Applied predictive modeling to analyze workforce performance and retention, supporting people and operational planning.</li>
                </ul>
            </div>

            <div class="role">
                <div class="role-header">
                    <span class="role-title">Maintenance Analysis Engineer</span>
                    <span class="role-date">Oct 2019 – Oct 2021</span>
                </div>
                <div class="role-company">Chandra Asri Group · Banten, Indonesia</div>
                <ul>
                    <li>Built analytical models and Tableau dashboards to support production and maintenance decision-making.</li>
                    <li>Redesigned maintenance reporting workflows to improve process clarity and operational tracking.</li>
                    <li>Implemented predictive maintenance monitoring, backlog tracking, and plant alert reporting.</li>
                </ul>
            </div>
        </section>

        <!-- Education -->
        <section>
            <div class="section-header">education</div>
            <div class="edu-item">
                <span class="degree"><strong>M.Sc. Data Science</strong> — The University of Edinburgh, United Kingdom</span>
                <span class="year">2024 – 2025</span>
            </div>
            <div class="edu-item">
                <span class="degree"><strong>B.Eng. Chemical Engineering</strong> — Institut Teknologi Sepuluh Nopember, Indonesia</span>
                <span class="year">2015 – 2019</span>
            </div>
        </section>

        <!-- Technologies -->
        <section>
            <div class="section-header">technologies</div>
            <div class="tech-category">
                <div class="tech-label">Languages</div>
                <div class="pills">
                    <span class="pill">Python</span>
                    <span class="pill">SQL</span>
                    <span class="pill">Scala</span>
                    <span class="pill">R</span>
                    <span class="pill">JavaScript</span>
                </div>
            </div>
            <div class="tech-category">
                <div class="tech-label">Technologies</div>
                <div class="pills">
                    <span class="pill">PyTorch</span>
                    <span class="pill">scikit-learn</span>
                    <span class="pill">OpenCV</span>
                    <span class="pill">BigQuery</span>
                    <span class="pill">Postgres</span>
                    <span class="pill">Tableau</span>
                    <span class="pill">Power BI</span>
                    <span class="pill">Looker Studio</span>
                    <span class="pill">Vertex AI</span>
                    <span class="pill">GCP</span>
                    <span class="pill">n8n</span>
                    <span class="pill">APIs</span>
                </div>
            </div>
            <div class="tech-category">
                <div class="tech-label">Other</div>
                <div class="pills">
                    <span class="pill">Generative AI</span>
                    <span class="pill">LLMs</span>
                    <span class="pill">RAG</span>
                    <span class="pill">LangChain</span>
                    <span class="pill">LangGraph</span>
                    <span class="pill">ETL</span>
                    <span class="pill">Data Modeling</span>
                    <span class="pill">A/B Testing</span>
                    <span class="pill">Web Scraping</span>
                </div>
            </div>
        </section>
    </div>
</body>
</html>
```

- [ ] **Step 2: Open `resume.html` in browser and verify**

```bash
open resume.html
```

Verify: dark background, grain overlay, back link + download button, intro with gradient name, all 5 roles with bullets, education, tech pills. Scrollable. Matches the approved mockup.

- [ ] **Step 3: Commit**

```bash
git add resume.html
git commit -m "feat: add resume page with full content"
```

---

### Task 6: Create `assets/` directory and update `.gitignore`

**Files:**
- Create: `assets/` directory
- Modify: `.gitignore`

- [ ] **Step 1: Create `assets/` directory with a `.gitkeep`**

```bash
mkdir -p assets
touch assets/.gitkeep
```

The user will add `resume.pdf` here before deployment.

- [ ] **Step 2: Add `.superpowers/` to `.gitignore`**

Append to the existing `.gitignore`:

```
# Superpowers brainstorming
.superpowers/
```

- [ ] **Step 3: Commit**

```bash
git add assets/.gitkeep .gitignore
git commit -m "chore: create assets directory, add .superpowers to gitignore"
```

---

### Task 7: Final verification

- [ ] **Step 1: Verify `index.html` in browser**

```bash
open index.html
```

Check: looks identical to the original, with "resume" link added. Clicking "resume" navigates to `resume.html`.

- [ ] **Step 2: Verify `resume.html` in browser**

Check: all sections render correctly. "← atoue.io" links back to `index.html`. "download pdf" links to `assets/resume.pdf`. Page scrolls. Responsive at narrow widths (use browser dev tools).

- [ ] **Step 3: Verify file structure**

```bash
find . -not -path './.git/*' -not -path './.superpowers/*' -not -name '.DS_Store' | sort
```

Expected:
```
.
./README.md
./assets
./assets/.gitkeep
./css
./css/landing.css
./css/resume.css
./css/shared.css
./docs
./docs/superpowers
./docs/superpowers/plans
./docs/superpowers/plans/2026-04-03-resume-page-and-restructure.md
./docs/superpowers/specs
./docs/superpowers/specs/2026-04-03-resume-page-and-restructure-design.md
./index.html
./resume.html
./.gitignore
```
