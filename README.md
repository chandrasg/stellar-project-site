# STELLAR Project Website

**Steering-Vector Enhanced LLM Agents for Realistic Digital Twins in Mental Health**

A [Wellcome Trust](https://wellcome.org)-funded collaboration between NYU, University of Pennsylvania, and the Linguistic Data Consortium.

## Quick Start

```bash
# Clone and serve locally
git clone https://github.com/YOUR_ORG/stellar-project-site.git
cd stellar-project-site
npx serve src/
# Open http://localhost:3000
```

## How Content Works

All site content lives in `/data/` as JSON files. The site reads from these — **never edit HTML to change content**. This means anyone on the team can update the site by editing a JSON file and pushing.

| File | What it controls |
|------|-----------------|
| `data/team.json` | Team members, roles, bios, photos, links |
| `data/publications.json` | Selected publications with DOIs |
| `data/positions.json` | Open positions and descriptions |
| `data/project.json` | Project description, aims, funder info |

## For Collaborators: Editing Content

### Update a team member's bio
1. Open `data/team.json`
2. Find the person by name
3. Edit the `bio` field
4. Commit and push — site rebuilds automatically

### Add a publication
1. Open `data/publications.json`
2. Add a new entry following the existing schema (title, authors, venue, year, doi)
3. Commit and push

### Update open positions
1. Open `data/positions.json`
2. Edit, add, or remove entries
3. Update `active: false` to hide a filled position without deleting it

## Deployment

### GitHub Pages (Production)
1. Push to `main` branch
2. Settings → Pages → Deploy from branch → `main` / root
3. Live at `https://YOUR_ORG.github.io/stellar-project-site/`

### Vercel (Staging)
Connected to the repo. Every PR gets a preview URL automatically.

### Custom Domain
1. Add domain to `CNAME` file
2. Configure DNS: CNAME record → `YOUR_ORG.github.io`
3. Enable HTTPS in GitHub Pages settings

## Building with the Agent Pipeline

If you're using Claude Code with the agent pipeline:

```bash
# Run the full pipeline
cc "Build the STELLAR site using /agents/ pipeline"

# Run a single agent
cc "Run the SEO review agent on the current site"

# Update data only
cc "Research agent: update publications from Semantic Scholar for all team members"
```

See `/agents/README.md` for full pipeline documentation.

## Project Structure

```
├── CLAUDE.md              # Global Claude Code instructions
├── README.md              # This file
├── .nojekyll              # GitHub Pages config
├── agents/                # Agent pipeline instructions
│   ├── README.md          # Orchestration docs
│   ├── 01-research.md     # Data gathering
│   ├── 02-design.md       # Design system
│   ├── 03-develop.md      # Build
│   ├── 04-review-design.md
│   ├── 05-review-content.md
│   ├── 06-review-seo.md
│   └── 07-review-visual.md
├── data/                  # Content (source of truth)
│   ├── README.md          # JSON schemas
│   ├── project.json
│   ├── team.json
│   ├── publications.json
│   └── positions.json
├── src/                   # Site source
│   ├── README.md          # Component architecture
│   └── index.html
└── assets/                # Static files
    ├── README.md          # Image specs
    └── images/
```

## TODO

**Before going public:**
- [ ] Replace `YOUR_ORG` in this README with the actual GitHub org/username
- [ ] Replace Google Form placeholder URL in `data/positions.json` → update `application_url`
- [ ] Add Wellcome Trust logo to `assets/images/` (pending brand approval from wellcome.org/brand)
- [ ] Set up custom domain — add `CNAME` file, configure DNS

**Already done:**
- [x] Team headshots — 6 of 10 members have verified photo URLs in `data/team.json`
- [x] Publication DOIs verified via Semantic Scholar and OpenAlex (12 papers)
- [x] Open Graph and Twitter Card meta tags
- [x] schema.org JSON-LD structured data (ResearchProject, ScholarlyArticle, JobPosting)

## License

Content © 2026 STELLAR Project. All rights reserved.
