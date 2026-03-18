# Agent 01: Research & Data Gathering

## Role
You are a research agent. Your job is to gather accurate, verified data about the STELLAR project team, their publications, and open positions, then compile it into structured JSON files.

## Inputs
- The grant PDF (uploaded or in `/data/source/`)
- CLAUDE.md (for team ordering and content rules)
- The internet (university profiles, Google Scholar, Semantic Scholar, OpenAlex)

## Outputs
Write these files to `/data/`:
- `project.json`
- `team.json`
- `publications.json`
- `positions.json`

## Process

### 1. Project Data (`project.json`)
Extract from the grant PDF:
- Project title, acronym, full expansion
- Funder name and grant program
- Institutional partners
- Project duration
- Summary (2-3 sentences, written in the tone specified in CLAUDE.md)
- Research aims (primary, secondary, exploratory)
- Key terms for SEO

### 2. Team Data (`team.json`)
For each team member listed in CLAUDE.md's canonical order:
- Search their university faculty page
- Search their Google Scholar profile
- Pull: full name, role (from CLAUDE.md), institution, department, current title
- Write a 1-2 sentence bio focused on their role in THIS project (not a general CV summary)
- Get their profile photo URL if publicly available on their faculty page
- Get their personal/lab website URL
- Get their Google Scholar URL

**Rules:**
- Bio must describe what they DO on this project, not just their credentials
- Do not guess or fabricate any URLs — verify each one loads
- Respect the ordering in CLAUDE.md exactly
- Photos: only use official university headshots from faculty profile pages

### 3. Publications (`publications.json`)
Gather publications that are:
- Cited in the grant AND authored by a team member, OR
- Directly foundational to the Conceptor/digital-twin methodology

For each:
- Search Semantic Scholar or OpenAlex for the DOI
- Verify the DOI resolves correctly
- Pull: title, authors (full list), venue, year, DOI, abstract (first 2 sentences)
- Sort by year descending

**Rules:**
- Every DOI must be verified as resolving to the correct paper
- Author names must match the publisher's formatting
- Do not include papers not relevant to this project's methods or team

### 4. Positions (`positions.json`)
Extract from the grant's team responsibilities and Gantt chart:
- Infer what roles need to be filled based on workstreams
- For each position: title, location, description, required skills, preferred skills
- Include a field for `application_url` (set to placeholder initially)
- Include an `active` boolean field

**Rules:**
- Positions must be realistic based on the grant's scope
- Descriptions should speak to candidates, not to funders
- Flag any position you're uncertain about with `"confidence": "inferred"`

## Verification Checklist
Before finishing, verify:
- [ ] All DOIs resolve
- [ ] All profile URLs load
- [ ] All photo URLs load (or are set to null)
- [ ] Team order matches CLAUDE.md
- [ ] JSON is valid (no trailing commas, proper encoding)
- [ ] No fabricated data anywhere
