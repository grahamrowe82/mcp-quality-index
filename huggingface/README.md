---
license: cc-by-4.0
task_categories:
  - text-classification
  - feature-extraction
tags:
  - mcp
  - model-context-protocol
  - open-source
  - quality-scores
  - developer-tools
  - ai-ecosystem
pretty_name: MCP Quality Index
size_categories:
  - 10K<n<100K
source_datasets:
  - original
---

# MCP Quality Index

Daily-updated quality scores for 12,000+ MCP (Model Context Protocol) server repositories.

## Dataset description

Every MCP registry today is a flat catalog. None of them tell you whether a server is maintained, adopted, or safe to depend on. This dataset scores every MCP-domain repository on GitHub across four dimensions: maintenance, adoption, maturity, and community.

## Files

| File | Records | Description |
|---|---|---|
| `mcp-scores.json` | 12,653 | Quality scores with component breakdown and risk flags |
| `mcp-repos.json` | 12,512 | All active MCP repos with GitHub + package metrics |
| `projects.json` | 441 | Tracked AI projects with traction scores and velocity |

## Scoring model

Each repo receives a composite quality score (0-100) from four equally-weighted components:

- **Maintenance** (0-25): commit activity + push recency
- **Adoption** (0-25): stars + downloads + reverse dependents
- **Maturity** (0-25): license + published package + repo age
- **Community** (0-25): forks + fork-to-star ratio

Scores map to tiers: **Verified** (70+), **Established** (50-69), **Emerging** (30-49), **Experimental** (<30).

Full methodology: [METHODOLOGY.md](https://github.com/grahamrowe82/mcp-quality-index/blob/main/METHODOLOGY.md)

## Source

Data is produced by [PT-Edge](https://github.com/grahamrowe82/pt-edge), which tracks 166,000+ AI repositories across GitHub, PyPI, npm, Docker Hub, HuggingFace, and Hacker News.

## Update frequency

Daily at approximately 06:00 UTC.

## Citation

```bibtex
@misc{mcp-quality-index-2026,
  title={MCP Quality Index},
  author={PT-Edge},
  year={2026},
  url={https://github.com/grahamrowe82/mcp-quality-index}
}
```
