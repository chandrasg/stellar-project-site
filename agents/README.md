# Agent Pipeline

## Overview

The site is built by a sequence of specialized agents, each with a narrow mandate. Constraints produce quality — a focused agent making one kind of decision outperforms a general agent told "make it good."

## Pipeline Order

```
01-research  →  02-design  →  03-develop  →  04-review-design  →  05-review-content  →  06-review-seo  →  07-review-visual
   (data)        (system)      (build)        (iterate)            (iterate)             (iterate)          (iterate)
```

### Phase 1: Build (Sequential, one pass each)
| Agent | Input | Output | Model |
|-------|-------|--------|-------|
| 01-research | Grant PDF, team URLs, Scholar profiles | `/data/*.json` | Opus (needs reasoning) |
| 02-design | CLAUDE.md, `/data/` | Design tokens, component specs in `/src/` | Opus (creative decisions) |
| 03-develop | Design specs, `/data/`, CLAUDE.md | Complete site in `/src/index.html` | Opus (complex build) |

### Phase 2: Review (Parallel-capable, multiple passes each)
| Agent | Focus | Edit Rule | Model |
|-------|-------|-----------|-------|
| 04-review-design | Visual consistency, spacing, typography | One fix per run | Sonnet |
| 05-review-content | Accuracy against source data, broken links | One fix per run | Sonnet |
| 06-review-seo | Meta tags, structured data, performance | One fix per run | Sonnet |
| 07-review-visual | Screenshots → visual bugs, responsive issues | One fix per run | Sonnet |

## Running Agents

### Full pipeline
```
Run the STELLAR site build pipeline from 01-research through 07-review-visual.
```

### Single agent
```
Run agent 05-review-content against the current site in /src/
```

### Review loop
Review agents (04-07) should run 3-5 times each until they report "no issues found." If an agent keeps finding issues after 5 runs, flag for human review.

## Rules for All Agents

1. **Read CLAUDE.md first.** Every agent starts by reading the root CLAUDE.md.
2. **Read your agent file.** Then read your specific instruction file in `/agents/`.
3. **Respect the data layer.** Content changes go in `/data/*.json`, never in HTML.
4. **One concern per agent.** Don't fix SEO issues in the design review agent.
5. **Log what you did.** Each agent appends to `/agents/build-log.md` with timestamp, agent name, and what changed.
6. **Don't break what works.** Review agents must verify their fix didn't introduce regressions.
