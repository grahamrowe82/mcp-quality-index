# mcp-scores.json schema

Quality scores for MCP server repositories. See [METHODOLOGY.md](../METHODOLOGY.md) for how scores are calculated.

| Field | Type | Description | Example |
|---|---|---|---|
| `full_name` | string | GitHub owner/repo | `"n8n-io/n8n"` |
| `name` | string | Repository name | `"n8n"` |
| `description` | string | Repository description | `"Fair-code workflow automation..."` |
| `stars` | integer | GitHub star count | `72841` |
| `forks` | integer | GitHub fork count | `19532` |
| `language` | string \| null | Primary programming language | `"TypeScript"` |
| `license` | string \| null | License identifier | `"Apache-2.0"` |
| `archived` | boolean | Whether the repo is archived | `false` |
| `subcategory` | string \| null | MCP classification | `"framework"` |
| `last_pushed_at` | string \| null | ISO 8601 timestamp of last push | `"2026-03-26T14:30:00+00:00"` |
| `pypi_package` | string \| null | PyPI package name, if published | `"n8n"` |
| `npm_package` | string \| null | npm package name, if published | `"n8n"` |
| `downloads_monthly` | integer | Combined monthly downloads (PyPI + npm) | `1547893` |
| `dependency_count` | integer | Number of declared dependencies | `42` |
| `commits_30d` | integer | Commits in the last 30 days | `289` |
| `reverse_dep_count` | integer | Repos that depend on this project | `15` |
| `maintenance_score` | integer | 0-25. Commit activity + push recency | `25` |
| `adoption_score` | integer | 0-25. Stars + downloads + dependents | `20` |
| `maturity_score` | integer | 0-25. License + package + age | `18` |
| `community_score` | integer | 0-25. Forks + fork-to-star ratio | `25` |
| `quality_score` | integer | 0-100. Sum of the four components | `88` |
| `quality_tier` | string | `"verified"` \| `"established"` \| `"emerging"` \| `"experimental"` | `"verified"` |
| `risk_flags` | array of strings | Applicable risk flags (see Methodology) | `[]` |

Records are sorted by `quality_score` descending.
