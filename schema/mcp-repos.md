# mcp-repos.json schema

All active (non-archived) MCP-domain repositories with GitHub and package metrics.

| Field | Type | Description | Example |
|---|---|---|---|
| `full_name` | string | GitHub owner/repo | `"n8n-io/n8n"` |
| `name` | string | Repository name | `"n8n"` |
| `description` | string | Repository description | `"Fair-code workflow automation..."` |
| `stars` | integer | GitHub star count | `72841` |
| `forks` | integer | GitHub fork count | `19532` |
| `language` | string \| null | Primary programming language | `"TypeScript"` |
| `topics` | array of strings | GitHub topics | `["ai", "mcp", "mcp-server"]` |
| `license` | string \| null | License identifier | `"Apache-2.0"` |
| `last_pushed_at` | string \| null | ISO 8601 timestamp of last push | `"2026-03-26T14:30:00+00:00"` |
| `archived` | boolean | Always `false` (archived repos are excluded) | `false` |
| `subcategory` | string \| null | MCP classification | `"gateway"` |
| `downloads_monthly` | integer | Combined monthly downloads (PyPI + npm) | `1547893` |
| `dependency_count` | integer | Number of declared dependencies | `42` |
| `pypi_package` | string \| null | PyPI package name, if published | `null` |
| `npm_package` | string \| null | npm package name, if published | `"n8n"` |
| `commits_30d` | integer | Commits in the last 30 days | `289` |

Records are sorted by `stars` descending.
