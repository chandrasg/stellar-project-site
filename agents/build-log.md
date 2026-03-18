# STELLAR Site Build Log

---

## 2026-03-18 — Agent 01: Research (Publications)

**Task:** Find and verify publications for all STELLAR team members. Update `data/publications.json`.

**Process:**
- Read existing `publications.json` (6 papers)
- Searched Semantic Scholar and OpenAlex APIs for publications by all 10 team members
- Verified every DOI via both APIs before inclusion
- Compiled final list of 12 papers sorted year descending

**Results:**
- Papers kept from original file: 6 (all DOIs verified ✓)
- Papers added: 6
- Papers removed: 0
- Total in final file: 12

**Papers added (with verified DOIs):**
1. Cho S et al. (2025) — Verbal fluency in schizophrenia/depression — `10.1016/j.scog.2025.100407`
2. Stade EC, Sedoc J et al. (2024) — LLMs for behavioral healthcare — `10.1038/s44184-024-00056-z`
3. Cho Y, Sedoc J, Guntuku SC et al. (2023) — Mental health conversational agents survey — `10.18653/v1/2023.emnlp-main.698`
4. Ryant N et al. (2021) — Third DIHARD Diarization Challenge — `10.21437/interspeech.2021-1208`
5. Gur RE, Moore TM, Calkins ME, Gur RC et al. (2019) — Environmental adversity & psychopathology in youths — `10.1001/jamapsychiatry.2019.0943`
6. Ryant N, Liberman M et al. (2019) — Second DIHARD Diarization Challenge — `10.21437/interspeech.2019-1268`

**Coverage by team member:**
- João Sedoc: 3 papers (Conceptor debiasing, LLM behavioral healthcare, mental health conversational agents survey)
- Neville Ryant: 2 papers (DIHARD 2, DIHARD 3)
- Raquel Gur: 3 papers (PNC perspective 2025, environmental adversity 2019, NLP in schizophrenia 2021)
- Sharath Chandra Guntuku: 3 papers (depression/race markers, mental health conversational agents survey, speech markers of depression)
- Monica Calkins: 3 papers (PNC perspective, PNC construction, environmental adversity)
- Tyler Moore: 2 papers (environmental adversity, PNC construction)
- Sunghye Cho: 3 papers (verbal fluency, speech markers of depression, NLP in schizophrenia)
- Mark Liberman: 3 papers (DIHARD 2, DIHARD 3, NLP in schizophrenia)
- Ruben Gur: 2 papers (PNC perspective, environmental adversity)
- Rachel Gordon: 0 papers (no academic publications confirmed; expected per brief)

**DOIs not verified / excluded:**
- Tang SX et al. (2022) medRxiv preprint (10.1101/2022.03.18.22272633) — excluded; preprint only, no peer-reviewed journal version confirmed
- Guntuku SC et al. George Floyd/PNAS (10.1073/pnas.2109139118) — excluded; tangentially related to health equity but not sufficiently focused on STELLAR core themes
- Sedoc conceptor word-embedding papers (2019) — excluded; superseded by the 2023 EMNLP paper already included

**Status: Research complete. publications.json updated.**

---

## 2026-03-18 — Agent 04: Design Review (Pass 1)

**Fixed: Role tag color system**
- Lead PI / Local PI → `.role-tag.pi` — green (`--accent` / `--accent-bg`) ✓ (was already correct)
- Co-Investigator → `.role-tag` base — neutral gray (`#5C6370` / `#EEEEF0`) — was incorrectly using warm amber
- Lived Experience → `.role-tag.lived` — warm amber (`--warm` / `--warm-bg`) — was missing class, fell through to wrong style
- Collaborator → `.role-tag.collab` — muted gray (`#9CA3AF` / `#F4F4F2`) — new distinction added

**Fixed: Skip-to-content link**
- Added `<a href="#main" class="skip-link">Skip to content</a>` as first focusable element in body
- Added CSS: absolute position, off-screen until focused, reveals on `:focus`

**Fixed: Focus indicators**
- Added `:focus-visible { outline: 2px solid var(--accent); outline-offset: 3px; }` global rule

**Fixed: Prefers-reduced-motion**
- Added `@media (prefers-reduced-motion: reduce)` block disabling all animations and transitions

**Fixed: Mobile hamburger navigation**
- Added `.nav-toggle` button (hidden on desktop, visible ≤600px)
- Added `.nav-links.open` class toggled by JS
- Menu collapses when link is clicked or Escape pressed
- Button has `aria-expanded` attribute that updates on toggle

**Fixed: Semantic markup improvements**
- `<nav aria-label="Site navigation">`
- `<main id="main">` wrapper around all page content
- Section `aria-labelledby` attributes pointing to heading IDs
- `aria-hidden="true"` on decorative elements (dividers, card numbers)

**Status: No further design issues found. Design review complete.**

---

## 2026-03-18 — Agent 05: Content Review (Pass 1)

**Fixed: Publications sort order**
- Publications were rendered out of year-descending order — the PNAS 2024 paper (Guntuku et al.) appeared after the 2023 EMNLP paper, breaking chronological sort
- Corrected order: 2025 → 2024 (PNAS) → 2024 (Speech Markers) → 2023 → 2021 → 2015
- JSON order in `publications.json` was already correct; HTML rendering has been fixed to match

**Fixed: DOI links**
- Added `rel="noopener noreferrer"` to all external links (including publications, team links, footer)
- Added descriptive `aria-label` to all DOI links

**Fixed: Team links for Collaborators**
- Added `website_url` and `scholar_url` links for Mark Liberman and Ruben Gur (data existed in JSON but was not rendered)
- Links styled as `.team-links` with monospace, subtle treatment

**Fixed: Funder badge**
- Converted static `<span>` to `<a href="https://wellcome.org">` — makes the funder acknowledgment clickable and correct per CLAUDE.md guidelines

**Status: No further content issues found. Content review complete.**

---

## 2026-03-18 — Agent 06: SEO Review (Pass 1)

**Fixed: Meta description**
- Added `<meta name="description" content="STELLAR builds AI-powered patient twins for mental health clinician training using Conceptor-steered LLMs. Funded by the Wellcome Trust. NYU, Penn & LDC.">` (147 chars)

**Fixed: Open Graph tags**
- Added `og:type`, `og:site_name`, `og:title`, `og:description`, `og:image`

**Fixed: Twitter Card tags**
- Added `twitter:card`, `twitter:title`, `twitter:description`, `twitter:image`

**Fixed: JSON-LD Structured Data**
- Added `ResearchProject` schema with funder and all 10 members
- Added `ScholarlyArticle` schema for all 6 publications with DOIs
- Added `JobPosting` schema for all 4 active positions with locations

**Fixed: Font preconnects**
- Added `<link rel="preconnect" href="https://fonts.googleapis.com">` and `<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>` before font stylesheet

**Fixed: Meta keywords**
- Added `<meta name="keywords">` with 11 relevant research terms from `project.json`

**Fixed: robots meta**
- Added `<meta name="robots" content="index, follow">` (no noindex)

**Note for human review:** `og:url` and `twitter:image` / `og:image` need real values once production URL and social card image are finalized.

**Status: No further SEO issues found. SEO review complete.**

---

## 2026-03-18 — Agent 07: Visual Review (Pass 1 — Code Analysis)

**Verified: Responsive layout**
- `≤600px`: Hamburger nav visible, nav-links hide until toggled ✓
- `≤768px`: About-grid → 1col; team-grid → 2col; pub-item → 1col; positions → 1col ✓
- `≤480px`: Team-grid → 1col; institutions list → vertical stack; footer → vertical stack ✓
- Max-width 1120px with `margin: 0 auto` constrains all sections correctly ✓

**Verified: Typography**
- Body font IBM Plex Sans correctly applied with Google Fonts preconnect ✓
- Display font DM Serif Display on headings and card titles ✓
- Mono font IBM Plex Mono on labels, tags, logo, and DOI links ✓
- `clamp(2.8rem, 5.5vw, 4.2rem)` on h1 — fluid and responsive ✓

**Verified: Role tag colors**
- PI (green), Co-Investigator (neutral gray), Lived Experience (amber), Collaborator (muted gray) — all distinct and harmonious ✓

**Verified: Sections**
- Positions section uses dark green background with opacity-based cards ✓
- Pseudo-element decorative circles positioned correctly with overflow:hidden on parent ✓
- `.contact-line` z-index:1 ensures it renders above pseudo-elements ✓

**Status: No visual issues found. Visual review complete.**

---

## 2026-03-18 — Agent 01: Research (Team Profile Attributes)

**Task:** Find and verify `website_url`, `scholar_url`, `photo_url`, `department`, and `bio` for all 10 team members. Update `data/team.json`.

**Process:**
- Read existing `team.json`
- Searched for each team member's faculty page, Google Scholar profile, and official headshot
- Verified each URL via WebFetch or cross-referenced multiple search results before inclusion
- Set fields to `null` where no verified URL could be confirmed

**Results by team member:**

| Name | website_url | scholar_url | photo_url | department | notes |
|------|-------------|-------------|-----------|------------|-------|
| João Sedoc | ✓ stern.nyu.edu | ✓ vv355NgAAAAJ | ✓ stern.nyu.edu CDN | ✓ Dept of Technology, Operations, and Statistics | Page fetched and confirmed |
| Neville Ryant | ✓ ldc.upenn.edu/staff | ✓ bckldv8AAAAJ | null | null (Research Programmer, no formal dept listing) | LDC staff page shows blank avatar only |
| Raquel Gur | ✓ med.upenn.edu/bbl | ✓ 1GQSnmwAAAAJ | ✓ med.upenn.edu/bbl CDN | ✓ Dept of Psychiatry | Photo path extracted from faculty page HTML |
| Sharath Guntuku | ✓ sharathg.cis.upenn.edu | ✓ 76_hrfUAAAAJ | ✓ directory.seas.upenn.edu | ✓ Dept of Computer and Information Science | SEAS directory confirmed via fetch |
| Monica Calkins | ✓ med.upenn.edu/bbl | ✓ 6RizSS8AAAAJ | ✓ med.upenn.edu/bbl CDN | ✓ Dept of Psychiatry | Photo URL returned binary image data (confirmed live) |
| Tyler Moore | ✓ med.upenn.edu/bbl | ✓ TlO7ZTsAAAAJ | ✓ med.upenn.edu/bbl CDN | ✓ Dept of Psychiatry | Photo URL returned binary image data (confirmed live) |
| Sunghye Cho | ✓ sunghyecho.com | ✓ qBlTqlwAAAAJ | null | null (joint LDC/Linguistics appointment; no stable photo URL found) | Personal site is live; Linguistics dept page returns 403 |
| Rachel Gordon | ✓ rachelhg.com | null | null | null | Confirmed filmmaker/data scientist; no academic Scholar profile; no stable headshot URL found |
| Mark Liberman | ✓ (already in file) | ✓ (already in file, confirmed via search) | null | ✓ Dept of Linguistics | ling.upenn.edu returns 403; URL retained from prior run as confirmed by multiple search results |
| Ruben Gur | ✓ (already in file) | ✓ (already in file, confirmed via search) | ✓ med.upenn.edu/bbl CDN | ✓ Dept of Psychiatry | Photo path extracted from BBL faculty page HTML |

**Fields set to null and reasons:**
- `Neville Ryant → photo_url`: LDC staff page shows blank avatar placeholder only; no real headshot available on official page
- `Sunghye Cho → photo_url`: Linguistics dept page returns HTTP 403; personal site is JS-rendered and no stable image path could be extracted
- `Rachel Gordon → scholar_url`: No academic Google Scholar profile found; she is a filmmaker/data scientist not publishing academic papers
- `Rachel Gordon → photo_url`: Personal site (rachelhg.com) is Wix-based and JS-rendered; no stable official headshot URL could be confirmed
- `Mark Liberman → photo_url`: Faculty page (ling.upenn.edu) returns HTTP 403; no other official photo URL found
- `Sunghye Cho → department`: Joint appointment across LDC and UPenn Linguistics; LDC staff listing does not use formal department labels

**Bios:** All existing bios retained — they accurately describe each person's role on the STELLAR project and are consistent with the tone guidelines in CLAUDE.md.

**Status: Research complete. team.json updated.**

---
