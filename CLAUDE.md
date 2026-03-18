# STELLAR Project Site

## What This Is
Website for a Wellcome Trust-funded research project: STELLAR (Steering-Vector Enhanced LLM Agents for Realistic Digital Twins in Mental Health). Multi-institutional collaboration between NYU, University of Pennsylvania, and the Linguistic Data Consortium.

The site serves three audiences:
1. **Potential hires** — postdocs, research scientists, engineers, coordinators
2. **Funders and program officers** — Wellcome Trust, future grant reviewers
3. **Academic collaborators** — people who might use or extend the Conceptor framework

## Architecture

```
/data/       → JSON files are the single source of truth for all content
/src/        → Site source code (HTML/CSS/JS or framework)
/assets/     → Images, fonts, static files
/agents/     → Agent instruction files for the build pipeline
```

**Critical rule**: Never hardcode content into HTML. All dynamic content (team, publications, positions, project details) lives in `/data/*.json`. The site reads from these files. To update content, edit JSON — not markup.

## Design System

### Aesthetic Direction
Editorial academic — think Wellcome Trust's own site, Nature, or the Stanford HAI site. Clean, high-trust, sophisticated without being cold. NOT generic SaaS landing page energy. 

### Typography
- Display/headings: Serif with character (DM Serif Display, Playfair Display, or similar)
- Body: Humanist sans-serif (IBM Plex Sans, Source Sans, or similar)
- Code/labels: Monospace (IBM Plex Mono, JetBrains Mono, or similar)
- Scale: Use a modular scale (1.25 ratio). Base 16px.

### Color
- Primary palette: Deep greens and warm neutrals. NOT blue-purple tech gradients. Take design cues from Penn Engineering and NYU Stern websites.
- Accent: One warm tone (amber/terracotta range) for tags and highlights.
- Background: Off-white, never pure white (#FAFAF7 range).
- Text: Near-black (#1A1A1A), never pure black.
- Ensure WCAG 2.1 AA contrast ratios on all text (4.5:1 body, 3:1 large).

### Layout
- Max content width: 1120px
- Generous whitespace. Let the content breathe.
- Mobile-first responsive. Test at 320px, 768px, 1024px, 1440px.
- No horizontal scroll at any breakpoint.

## Content Rules

### Team Ordering
Team order is intentional and reflects PI hierarchy. NEVER reorder without explicit instruction.

Current canonical order:
1. João Sedoc — Lead PI (NYU)
2. Neville Ryant — Lead PI (UPenn & LDC)
3. Raquel Gur — Local PI, Penn Medicine
4. Sharath Chandra Guntuku — Local PI, Penn Engineering
5. Monica Calkins — Co-Investigator
6. Tyler Moore — Co-Investigator
7. Sunghye Cho — Co-Investigator
8. Rachel Gordon — Lived Experience
9. Mark Liberman — Collaborator
10. Ruben Gur — Collaborator

### Tone
- Warm, direct, conversational. Not promotional.
- Lead with problems, not credentials.
- No hype language ("groundbreaking", "revolutionary", "cutting-edge").
- Understated endings. No hard sells.

### Citations
- All publication DOIs must be verified against Semantic Scholar, OpenAlex, or publisher sites.
- Never fabricate or guess citations.
- Author lists: Use abbreviated format (Last INITIALS) for >3 authors, then "et al."

### Funder Acknowledgment
Always credit: "Funded by the Wellcome Trust" with link to wellcome.org.
Follow Wellcome's brand guidelines for logo usage if displaying their mark.

## Accessibility Requirements (Non-Negotiable)
- Semantic HTML: proper heading hierarchy (h1 → h2 → h3, no skipping)
- All images have descriptive alt text
- All interactive elements keyboard-accessible
- Focus indicators visible
- Color is never the sole means of conveying information
- Reduced motion media query respected for animations
- Lang attribute set on <html>
- Skip-to-content link

## Performance Targets
- Lighthouse Performance: >90
- Lighthouse Accessibility: >95
- LCP: <2.5s
- CLS: <0.1
- No render-blocking resources
- Images lazy-loaded below the fold
- Fonts preloaded or system-fallback first

## Deployment
- **Production**: GitHub Pages from `main` branch, root `/`
- **Staging/Preview**: Vercel auto-deploy on PR
- `.nojekyll` file must exist in root
- CNAME file if custom domain is configured

## Agent Pipeline
Agents run sequentially. See `/agents/README.md` for orchestration.
Each agent reads its instruction file and the relevant data files.
Each review agent makes ONE focused edit per run and can run multiple times.
