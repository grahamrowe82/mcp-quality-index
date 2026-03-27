# projects.json schema

Tracked AI projects with traction scores, lifecycle stages, and velocity metrics. This dataset covers the broader AI ecosystem (441 projects), not just MCP servers.

| Field | Type | Description | Example |
|---|---|---|---|
| `name` | string | Project name | `"n8n"` |
| `slug` | string | URL-safe identifier | `"n8n"` |
| `category` | string | Project category | `"tool"` |
| `domain` | string | Ecosystem domain | `"mcp"` |
| `stack_layer` | string | Position in the AI stack | `"orchestration"` |
| `lab_name` | string \| null | Associated research lab | `null` |
| `stars` | integer | GitHub star count | `72841` |
| `forks` | integer | GitHub fork count | `19532` |
| `monthly_downloads` | integer | Combined monthly downloads | `1547893` |
| `commits_30d` | integer | Commits in the last 30 days | `289` |
| `stars_7d_delta` | integer | Star count change over 7 days | `1250` |
| `stars_30d_delta` | integer | Star count change over 30 days | `4800` |
| `dl_30d_delta` | integer | Download count change over 30 days | `120000` |
| `commits_7d_delta` | integer | Commit count change over 7 days | `45` |
| `commits_30d_delta` | integer | Commit count change over 30 days | `20` |
| `contributors_30d_delta` | integer | New contributors over 30 days | `5` |
| `hype_ratio` | float | Star volatility relative to base | `0.0009` |
| `hype_bucket` | string | Hype classification | `"quiet_adoption"` |
| `velocity_band` | string | Development velocity category | `"hyperspeed"` |
| `commits_per_contributor` | float | Activity density metric | `3.2` |
| `development_pace` | string | Pace classification | `"human"` |
| `fork_star_ratio` | float | Forks divided by stars | `0.27` |
| `lifecycle_stage` | string | Project maturity stage | `"established"` |
| `tier` | integer | Traction tier (1 = highest) | `1` |
| `traction_score` | integer | 0-100 overall traction score | `100` |
| `traction_bucket` | string | Traction classification | `"infrastructure"` |
| `dl_trend` | string | Download trend direction | `"stable"` |
| `dl_weekly_velocity` | float | Weekly download velocity | `0.02` |
| `last_commit_at` | string \| null | ISO 8601 timestamp of last commit | `"2026-03-26T10:00:00+00:00"` |
| `last_release_at` | string \| null | ISO 8601 timestamp of last release | `"2026-03-20T08:00:00+00:00"` |
| `days_since_release` | integer \| null | Days since last release | `7` |

Records are sorted by `traction_score` descending.
