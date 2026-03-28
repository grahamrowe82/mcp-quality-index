[![Last Updated](https://img.shields.io/github/last-commit/grahamrowe82/mcp-quality-index?label=last%20updated)](https://github.com/grahamrowe82/mcp-quality-index/commits/main)
[![Servers Scored](https://img.shields.io/badge/servers_scored-13655-blue)](#datasets)
[![License](https://img.shields.io/github/license/grahamrowe82/mcp-quality-index)](LICENSE)

# MCP Quality Index

Daily-updated quality scores for 12,653+ MCP server repositories. Machine-readable JSON. No auth required.

## What is this?

Every MCP registry today is a flat catalog — name, description, maybe a link. None of them tell you whether a server is maintained, adopted, or safe to depend on.

This dataset scores every MCP-domain repository on GitHub across four dimensions:

| Component | Range | What it measures |
|-----------|-------|-----------------|
| **Maintenance** | 0-25 | Commit activity, push recency, archived status |
| **Adoption** | 0-25 | Stars, package downloads, reverse dependents |
| **Maturity** | 0-25 | License, published package (PyPI/npm), repo age |
| **Community** | 0-25 | Forks, fork-to-star ratio |

The composite **quality score** (0-100) classifies each server into a tier:

| Tier | Score | Count | Description |
|------|-------|-------|-------------|
| **Verified** | 70+ | 53 | Strong across all dimensions |
| **Established** | 50-69 | 680 | Solid but gaps in one area |
| **Emerging** | 30-49 | 3,078 | Early-stage, some traction |
| **Experimental** | <30 | 8,842 | Minimal signals |

Risk flags are computed per repo: `archived`, `no_license`, `stale_6m`, `no_package`, `no_dependents`.

See [METHODOLOGY.md](METHODOLOGY.md) for the full scoring model, and [`schema/`](schema/) for field-level documentation.

## Datasets

All files are in [`data/`](data/):

| File | Records | Description |
|------|---------|-------------|
| [`mcp-scores.json`](data/mcp-scores.json) | 12,653 | Quality scores with component breakdown and risk flags |
| [`mcp-repos.json`](data/mcp-repos.json) | 12,512 | All active MCP repos with GitHub + package metrics |
| [`projects.json`](data/projects.json) | 441 | Tracked AI projects with traction scores, lifecycle stages, velocity |
| [`metadata.json`](data/metadata.json) | — | Export timestamp, record counts, schema version |

## Usage

Fetch the raw JSON directly:

```bash
curl -s https://raw.githubusercontent.com/grahamrowe82/mcp-quality-index/main/data/mcp-scores.json | jq '.[0]'
```

```json
{
  "full_name": "n8n-io/n8n",
  "quality_score": 88,
  "quality_tier": "verified",
  "maintenance_score": 25,
  "adoption_score": 20,
  "maturity_score": 18,
  "community_score": 25,
  "risk_flags": [],
  "stars": 72841,
  "downloads_monthly": 1547893,
  "commits_30d": 289
}
```

Filter verified servers with jq:

```bash
curl -s https://raw.githubusercontent.com/grahamrowe82/mcp-quality-index/main/data/mcp-scores.json \
  | jq '[.[] | select(.quality_tier == "verified")] | length'
```

## Live API

The same data is available via the PT-Edge API (no auth required):

```
GET https://mcp.phasetransitions.ai/api/v1/datasets/mcp-scores
GET https://mcp.phasetransitions.ai/api/v1/datasets/mcp-scores?quality_tier=verified
GET https://mcp.phasetransitions.ai/api/v1/datasets/mcp-scores?subcategory=gateway
GET https://mcp.phasetransitions.ai/api/v1/datasets/mcp-repos
GET https://mcp.phasetransitions.ai/api/v1/datasets/projects
```

## Update frequency

Data is refreshed daily from [PT-Edge](https://github.com/grahamrowe82/pt-edge), which tracks 166,000+ AI repositories across GitHub, PyPI, npm, Docker Hub, HuggingFace, and Hacker News.

## License

Data: [CC-BY-4.0](https://creativecommons.org/licenses/by/4.0/). Attribution: PT-Edge (https://github.com/grahamrowe82/pt-edge).
