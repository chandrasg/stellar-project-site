# Data Directory

This is the single source of truth for all site content. **Edit these files to update the site — never edit HTML directly.**

## Schemas

### `project.json`
```json
{
  "title": "string — full project title",
  "acronym": "string — STELLAR",
  "acronym_expansion": "string — what STELLAR stands for",
  "funder": "string — Wellcome Trust",
  "funder_url": "string — https://wellcome.org",
  "funder_program": "string — optional, specific grant program name",
  "duration": "string — e.g., 2026–2028",
  "summary": "string — 2-3 sentence project summary",
  "institutions": ["string — list of institutional partners"],
  "aims": {
    "primary": "string",
    "secondary": "string",
    "exploratory": "string"
  },
  "keywords": ["string — for meta tags and SEO"]
}
```

### `team.json`
```json
[
  {
    "name": "string — full name",
    "role": "string — Lead PI | Local PI | Co-Investigator | Lived Experience | Collaborator",
    "role_detail": "string — optional, e.g., 'Penn Medicine' or 'UPenn & LDC'",
    "institution": "string",
    "department": "string — optional",
    "bio": "string — 1-2 sentences about their role on THIS project",
    "photo_url": "string | null — URL to official headshot",
    "website_url": "string | null — personal or lab website",
    "scholar_url": "string | null — Google Scholar profile",
    "order": "integer — display order (1-indexed)"
  }
]
```

### `publications.json`
```json
[
  {
    "title": "string — full paper title",
    "authors": "string — formatted author list",
    "venue": "string — journal or conference name",
    "year": "integer",
    "doi": "string — full DOI (e.g., 10.1073/pnas.2319837121)",
    "doi_url": "string — full URL (e.g., https://doi.org/10.1073/pnas.2319837121)",
    "abstract_short": "string | null — first 1-2 sentences of abstract"
  }
]
```
Sorted by year descending, then alphabetically by first author within year.

### `positions.json`
```json
{
  "application_url": "string — Google Form or application portal URL",
  "positions": [
    {
      "title": "string — job title",
      "location": "string — e.g., NYU or Penn",
      "description": "string — 2-3 sentences about the role",
      "required_skills": ["string"],
      "preferred_skills": ["string"],
      "active": "boolean — true if currently hiring",
      "confidence": "string — 'confirmed' or 'inferred' (from grant)"
    }
  ]
}
```

## Rules
- All strings must be properly escaped JSON
- URLs must be verified as working
- Team order must match CLAUDE.md canonical order
- Do not include any private information (personal emails, phone numbers)
- Publications DOIs must be verified against the publisher
