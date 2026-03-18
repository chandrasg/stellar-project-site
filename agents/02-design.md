# Agent 02: Design System & Component Architecture

## Role
You are a design agent. Your job is to define the complete visual system for the site — not to write code, but to produce a design specification that the develop agent can implement precisely.

## Inputs
- CLAUDE.md (design principles, aesthetic direction, accessibility requirements)
- `/data/*.json` (to understand content volume and structure)
- Reference sites for inspiration (check these live):
  - https://wellcome.org (funder's own site)
  - https://hai.stanford.edu (Stanford HAI — academic + tech)
  - https://www.nature.com (editorial clarity)
  - https://www.allenai.org (AI research lab)

## Output
Write `/src/design-system.md` containing the full spec below.

## What to Define

### 1. Color Tokens
Define as CSS custom properties:
```
--color-bg-primary
--color-bg-secondary
--color-bg-accent
--color-text-primary
--color-text-secondary
--color-text-muted
--color-accent-primary
--color-accent-secondary
--color-border
--color-border-light
```
Verify all text/background combinations meet WCAG 2.1 AA (4.5:1 for body text, 3:1 for large text). Document the contrast ratio for each pair.

### 2. Typography Scale
Define font families, weights, and a size scale:
```
--font-display: [chosen serif]
--font-body: [chosen sans]
--font-mono: [chosen mono]

--text-xs:    0.75rem
--text-sm:    0.875rem
--text-base:  1rem
--text-lg:    1.125rem
--text-xl:    1.25rem
--text-2xl:   1.5rem
--text-3xl:   2rem
--text-4xl:   2.5rem
--text-hero:  clamp(2.5rem, 5vw, 4rem)
```
Specify line-height and letter-spacing for each scale step.

### 3. Spacing Scale
Use a consistent base unit (suggest 0.25rem = 4px):
```
--space-1: 0.25rem
--space-2: 0.5rem
--space-3: 0.75rem
--space-4: 1rem
... through --space-16: 4rem
--space-section: 5rem (vertical section padding)
```

### 4. Component Specs
For each component, define: layout, spacing, typography choices, colors, border radius, hover/focus states, responsive behavior.

**Components needed:**
- **Nav**: Fixed top, blurred background, logo left, links right, mobile hamburger
- **Hero**: Funder badge, h1 title, subtitle, lead paragraph, institution list
- **Section header**: Label (mono, uppercase), h2, optional description
- **About cards**: Grid of 2 columns, numbered, with h3 and description
- **Team cards**: Grid of 3-4 columns, role tag (color-coded by role type), name, affiliation, bio, optional photo
- **Publication items**: Year badge, title, authors, venue, DOI link
- **Positions section**: Dark/inverted background, position cards with title, location, description
- **Footer**: Two-column — copyright left, links right

### 5. Role Tag Colors
Define distinct but harmonious colors for each role type:
- Lead PI → accent green with green bg
- Local PI → accent green with green bg (same as Lead PI)
- Co-Investigator → default/neutral
- Lived Experience → warm tone
- Collaborator → muted/subtle

### 6. Responsive Breakpoints
```
--bp-mobile:  480px
--bp-tablet:  768px
--bp-desktop: 1024px
--bp-wide:    1440px
```
Document what changes at each breakpoint (grid columns, font sizes, padding).

### 7. Animation & Motion
- Page load: Staggered fade-up on hero elements (0.1s delay increments)
- Cards: Subtle border-color and shadow transition on hover (0.3s ease)
- Nav: Background blur on scroll
- Respect `prefers-reduced-motion`: disable all animations

### 8. Dark Mode (Optional, Stretch)
If implementing, define alternate color tokens under `@media (prefers-color-scheme: dark)`.

## Rules
- Every decision must trace back to CLAUDE.md's aesthetic direction
- Do not use any font listed as banned in CLAUDE.md (Inter, Roboto, Arial)
- Do not default to blue or purple as primary colors
- Test your color choices at https://webaim.org/resources/contrastchecker/
- Document WHY you made each choice, not just what it is
