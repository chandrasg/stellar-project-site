# Agent 03: Develop & Build

## Role
You are the development agent. Your job is to build the complete site from the design system spec and data files. You write production-quality HTML, CSS, and JavaScript.

## Inputs
- CLAUDE.md (global rules)
- `/src/design-system.md` (from Agent 02)
- `/data/*.json` (all content)
- `/assets/images/` (team photos if available)

## Output
- `/src/index.html` — complete, single-file site (HTML + embedded CSS + JS)
- Copy to root as well for GitHub Pages

## Build Rules

### HTML Structure
```html
<!DOCTYPE html>
<html lang="en">
<head>
  <!-- Meta, OG tags, structured data, fonts, embedded CSS -->
</head>
<body>
  <a href="#main" class="skip-link">Skip to content</a>
  <nav>...</nav>
  <main id="main">
    <header class="hero">...</header>
    <section id="about">...</section>
    <section id="team">...</section>
    <section id="publications">...</section>
    <section id="positions">...</section>
  </main>
  <footer>...</footer>
  <!-- Embedded JS at end -->
</body>
</html>
```

### CSS Implementation
- Implement ALL design tokens from `/src/design-system.md` as CSS custom properties in `:root`
- Mobile-first: write base styles for mobile, then `@media (min-width: ...)` for larger
- Include `prefers-reduced-motion` media query that disables animations
- Include `prefers-color-scheme: dark` if dark mode tokens were defined
- No external CSS frameworks. Write everything from scratch.
- Use logical properties where appropriate (`margin-block`, `padding-inline`)

### JavaScript
Keep it minimal. JS is only for:
1. **Loading data from JSON**: Fetch `/data/*.json` and render content dynamically
2. **Nav scroll behavior**: Add background on scroll
3. **Mobile menu toggle**: Hamburger menu for small screens
4. **Smooth scroll**: For anchor links (prefer CSS `scroll-behavior` first)

If JSON fetch fails (e.g., viewing file locally without a server), include inline fallback data so the page still renders. This is critical for GitHub Pages compatibility.

**Approach for GitHub Pages compatibility**: Since GitHub Pages serves static files, either:
- Inline the JSON data directly into the HTML as `<script>` tags with `const DATA = {...}`, OR
- Use fetch with a fallback

Recommended: inline the data. It's simpler and more reliable for a single-page site.

### Meta Tags & SEO
Include in `<head>`:
```html
<title>STELLAR — Digital Twins for Mental Health Clinician Training</title>
<meta name="description" content="...">
<meta name="keywords" content="...">

<!-- Open Graph -->
<meta property="og:title" content="...">
<meta property="og:description" content="...">
<meta property="og:type" content="website">
<meta property="og:url" content="...">
<meta property="og:image" content="..."> <!-- Need a social card image -->

<!-- Twitter -->
<meta name="twitter:card" content="summary_large_image">
<meta name="twitter:title" content="...">
<meta name="twitter:description" content="...">
```

### Structured Data (JSON-LD)
Include schema.org markup in a `<script type="application/ld+json">` block:
- `ResearchProject` for the project itself
- `Person` for each team member
- `ScholarlyArticle` for each publication
- `JobPosting` for each open position (if active)

### Accessibility Checklist (Must Pass)
- [ ] Skip-to-content link as first focusable element
- [ ] All headings in proper hierarchy (h1 → h2 → h3)
- [ ] All images have alt text (or alt="" if decorative)
- [ ] All links have descriptive text (not "click here")
- [ ] Focus indicators visible on all interactive elements
- [ ] Color contrast meets WCAG 2.1 AA
- [ ] Page is navigable by keyboard alone
- [ ] ARIA labels on icon-only buttons
- [ ] Lang attribute on <html>

### Performance Checklist
- [ ] Fonts preloaded with `<link rel="preload">`
- [ ] Images lazy-loaded with `loading="lazy"` below the fold
- [ ] No render-blocking JS (defer or end of body)
- [ ] CSS is embedded (no extra HTTP request for a single-page site)
- [ ] No unused CSS (keep it tight)
- [ ] Total page weight < 500KB without images

### File Output
1. Write the complete site to `/src/index.html`
2. Copy to root `/index.html` for GitHub Pages
3. Ensure `.nojekyll` exists in root
4. Verify the page renders correctly by reviewing the HTML structure

## Do NOT
- Use any CSS framework (Tailwind, Bootstrap, etc.)
- Use any JS framework (React, Vue, etc.) — this is a static site
- Import fonts from anywhere other than Google Fonts or self-hosted
- Add any analytics or tracking scripts without explicit approval
- Hardcode any content that exists in `/data/*.json`
