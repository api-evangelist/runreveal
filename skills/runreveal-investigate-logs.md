---
name: Investigate security logs with RunReveal
description: Query the RunReveal security data lake, inspect table schemas, and open an investigation from findings.
api: mcp/runreveal-mcp.yml
transport: https://api.runreveal.com/mcp
operations: [list_tables, get_table_schema, run_query, investigation_create]
scopes: [queries#read, investigations#edit]
---

# Investigate security logs with RunReveal

Use the RunReveal MCP server (`https://api.runreveal.com/mcp`, OAuth) or the local
CLI (`runreveal mcp`) with an API token. Select the target workspace first.

## Steps
1. **Discover data.** Call `list_tables` to see queryable tables, then
   `get_table_schema` on the table of interest to learn its columns.
2. **Query.** Call `run_query` with a SQL or PQL query (PQL compiles to SQL — see
   https://pql.dev). Scope by time window and filter to the entities under review.
3. **Pivot.** Refine `run_query` iteratively — join across sources, aggregate by
   actor/IP, and confirm a hypothesis.
4. **Open an investigation.** When findings warrant follow-up, call
   `investigation_create` to capture the query, context, and notes for the team.

## Rules
- Every tool requires the matching OAuth scope / API-token permission for the
  workspace (`queries#read` to query, `investigations#edit` to open one).
- All work is workspace-scoped; never assume a default workspace.
- Prefer narrow time ranges on `run_query` — the data lake is high-volume.
