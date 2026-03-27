# Methodology

How the MCP Quality Index scores 12,000+ MCP server repositories.

## What counts as an MCP server?

A repository is included if it matches any of the following:

- Has a GitHub topic containing `mcp-server`, `mcp`, or `model-context-protocol`
- Contains keywords in its name or description indicating MCP server functionality
- Is classified as MCP-domain by LLM-assisted detection (used for ambiguous cases)

Repositories are sourced exclusively from GitHub. GitLab, Codeberg, and other hosts are not currently tracked.

## Scoring model

Each repository is scored across four components, each worth 0-25 points, for a composite quality score of 0-100.

### Maintenance (0-25 points)

Measures whether the project is actively developed. Archived repositories score 0.

**Commit activity** (0-12 points):

| Commits in last 30 days | Points |
|---|---|
| 0 | 0 |
| 1-5 | 3 |
| 6-20 | 7 |
| 21-50 | 10 |
| 50+ | 12 |

**Push recency** (0-13 points):

| Last push | Points |
|---|---|
| Within 30 days | 13 |
| 31-90 days | 10 |
| 91-180 days | 6 |
| 181-365 days | 2 |
| Over 1 year / unknown | 0 |

### Adoption (0-25 points)

Measures whether anyone is actually using the project.

- **Stars** (0-10 points): `min(10, floor(ln(stars + 1) * 2))`
- **Monthly downloads** (0-10 points): `min(10, floor(ln(downloads + 1)))` — aggregated from PyPI and/or npm, whichever package is registered
- **Reverse dependents** (0-5 points): count of other tracked repositories that depend on this project's published package, capped at 5

### Maturity (0-25 points)

Measures whether the project has the hallmarks of a production-ready tool.

- **Has a license** (0 or 8 points): any license present in the repository
- **Published package** (0 or 9 points): available on PyPI and/or npm
- **Repository age** (0-8 points):

| Age | Points |
|---|---|
| Under 30 days | 1 |
| 30-90 days | 3 |
| 90-180 days | 5 |
| 180-365 days | 7 |
| Over 1 year | 8 |

### Community (0-25 points)

Measures whether the project has attracted external contributors and users.

- **Forks** (0-15 points): `min(15, floor(ln(forks + 1) * 3))`
- **Fork-to-star ratio** (0-10 points): `min(10, round(forks / stars * 50))` — a higher ratio suggests the project is being actively extended, not just starred

## Quality tiers

| Tier | Score range | Description |
|---|---|---|
| **Verified** | 70-100 | Strong signals across all four dimensions |
| **Established** | 50-69 | Solid overall, but gaps in one area |
| **Emerging** | 30-49 | Early-stage with some traction |
| **Experimental** | 0-29 | Minimal signals |

## Risk flags

Each repository is tagged with applicable risk flags:

| Flag | Condition |
|---|---|
| `archived` | Repository is archived on GitHub |
| `no_license` | No license file or license metadata |
| `stale_6m` | No push in the last 180 days |
| `no_package` | Not published on PyPI or npm |
| `no_dependents` | Zero tracked reverse dependents and zero declared dependencies |

## Data sources

- **GitHub API**: stars, forks, commits, push dates, topics, license, archived status
- **PyPI API**: monthly download counts for Python packages
- **npm API**: monthly download counts for JavaScript/TypeScript packages
- **Package dependency graphs**: reverse dependents computed from `package_deps` tracking across all 166,000+ tracked AI repositories

## Update frequency

Scores are refreshed daily at approximately 06:00 UTC as part of the [PT-Edge](https://github.com/grahamrowe82/pt-edge) ingest pipeline. The pipeline:

1. Ingests fresh data from GitHub, PyPI, and npm
2. Refreshes the materialized quality score view
3. Exports updated JSON to this repository

## Known limitations and biases

- **Log-scale scoring favours large projects**: A repo with 1,000 stars scores only moderately higher than one with 100 stars (logarithmic), but the gap between 0 and 10 stars is proportionally larger. This is intentional — it prevents mega-projects from dominating — but it means mid-tier scores compress together.
- **No code quality analysis**: The index measures external signals (activity, adoption, packaging) not code quality, test coverage, or security posture.
- **GitHub-only**: Repositories hosted on GitLab, Codeberg, or self-hosted instances are not included.
- **Age penalty for new projects**: A brand-new repository can score at most 1/8 on the age component of maturity, regardless of quality. This resolves over time.
- **Download counts vary by ecosystem**: PyPI and npm have different baseline download volumes. A package with 1,000 monthly downloads on PyPI is more notable than the same count on npm.
- **Fork-to-star ratio can mislead**: Tutorial repos and template repos have high fork ratios that inflate community scores without indicating genuine collaboration.
- **Subcategory classification is imperfect**: Some repositories may be miscategorised, particularly those that span multiple domains or have ambiguous descriptions.
