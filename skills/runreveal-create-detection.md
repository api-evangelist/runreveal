---
name: Create and route a RunReveal detection
description: Author a detection (native or Sigma), then wire its signals to a notification.
api: mcp/runreveal-mcp.yml
transport: https://api.runreveal.com/mcp
operations: [detections_create, sigma_create, detection_update, notification_send]
scopes: [queries#edit, notifications#edit, notifications#send]
---

# Create and route a RunReveal detection

Detection-as-code: author a detection over your logs and route its signals to the
right channel. Use the RunReveal MCP server or the `runreveal detections` CLI.

## Steps
1. **Draft the logic.** Validate the query with `run_query` against real data so
   the detection fires on true positives and stays quiet otherwise.
2. **Create the detection.** Call `detections_create` (native RunReveal detection)
   or `sigma_create` to import a Sigma-format rule.
3. **Tune.** Use `detection_update` (or `sigma_update`) to adjust thresholds,
   schedule, and severity after reviewing early signals.
4. **Route.** Wire matching signals to a destination and, when needed, call
   `notification_send` to deliver an alert (e.g. Slack).

## Rules
- Requires `queries#edit` to create/modify detections and `notifications#edit` /
  `notifications#send` to route and deliver alerts.
- Test detections against real log data before enabling — RunReveal supports
  detection testing (see docs `/how-to-guides/detections-signals-alerts-quick-start`).
- All operations are workspace-scoped.
