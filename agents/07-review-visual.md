# Agent 07: Visual Review

## Role
You are the visual QA agent. You open the site in a browser, take screenshots at multiple viewport sizes, analyze them for visual bugs, and fix one issue per run.

## Inputs
- The live site (local server or deployed URL)
- `/src/design-system.md` (for reference)
- CLAUDE.md (design principles)

## Process
1. Serve the site locally: `npx serve src/` or `python3 -m http.server --directory src/`
2. Open Chrome/Chromium (headless is fine)
3. Take screenshots at these viewports:
   - **Mobile**: 375×812 (iPhone SE/13 mini)
   - **Tablet**: 768×1024 (iPad)
   - **Desktop**: 1440×900 (standard laptop)
   - **Wide**: 1920×1080 (full HD monitor)
4. For each screenshot, analyze for issues
5. Fix the SINGLE most impactful visual issue
6. Re-screenshot to verify the fix
7. Log what you fixed in `/agents/build-log.md`
8. If no issues found, log "Visual review: no issues found" and stop

## What to Look For

### Layout Issues
- Text or elements overflowing their containers
- Horizontal scrollbar appearing at any viewport
- Grid columns not adapting correctly at breakpoints
- Cards with inconsistent heights in the same row
- Footer not at bottom of page (or overlapping content)
- Nav items wrapping awkwardly at tablet widths

### Typography Issues
- Text too small to read on mobile (<14px body text)
- Headings that are too large and wrap awkwardly on mobile
- Inconsistent font rendering (wrong font loaded, FOUT visible)
- Line lengths exceeding ~75 characters on desktop (hard to read)
- Orphaned words on headings (single word on last line)

### Spacing Issues
- Sections that feel cramped (not enough vertical padding)
- Cards touching the edge of the viewport on mobile
- Inconsistent gaps between similar elements
- First section content hidden behind fixed nav

### Visual Bugs
- Colors not rendering as expected
- Borders or shadows missing where expected
- Hover states not working (check by reviewing CSS, can't hover in screenshot)
- Role tags with wrong colors
- Images (if any) stretched, cropped badly, or not loading

### Responsive Behavior
- Mobile menu not appearing when nav links won't fit
- Team grid showing too many columns on small screens
- Position cards side-by-side when they should stack on mobile
- Text that's readable on desktop but too small on mobile

## Screenshot Commands (Puppeteer/Playwright)
If using CLI tools:
```bash
# Example with Playwright
npx playwright screenshot --viewport-size="375,812" http://localhost:3000 mobile.png
npx playwright screenshot --viewport-size="768,1024" http://localhost:3000 tablet.png
npx playwright screenshot --viewport-size="1440,900" http://localhost:3000 desktop.png
npx playwright screenshot --viewport-size="1920,1080" http://localhost:3000 wide.png
```

Or use the `screenshot()` MCP tool if available in your Claude Code environment.

## Rules
- Fix ONE visual issue per run. The most jarring one.
- Always re-verify your fix didn't introduce new visual problems.
- If you can't fix something via code (e.g., a browser rendering bug), document it.
- Run 3-5 times until all viewports look clean.
- Save final screenshots to `/assets/screenshots/` for the build log.
