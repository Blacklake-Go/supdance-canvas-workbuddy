# SupDance Canvas for WorkBuddy

WorkBuddy connector for the signed-in [SupDance Canvas](https://canvas.supdance.com/canvas). It uses one local stdio MCP Server and the SupDance Canvas Agent to read and operate the canvas open in the user's system browser.

## Package

- `connector-meta.json`: WorkBuddy marketplace metadata, bilingual examples, and minimum client version.
- `mcp.json`: starts the compact WorkBuddy Agent `0.1.7` GitHub release tarball with a WorkBuddy-managed Node.js runtime. Its package entry point disables restoration of Codex-only conversations.
- `icon.png`: SupDance artwork supplied by the publisher.
- `skills/supdance-canvas/SKILL.md`: connection, analysis, modification, and paid-generation guidance.

The connector source is maintained independently from the Codex plugin. Its Agent tarball is built from shared source and pins only the runtime dependencies required for the Canvas bridge.

## Connection

1. Install and connect the connector in WorkBuddy.
2. Ask WorkBuddy to open your recent SupDance canvas. `canvas_open` starts or reuses the loopback-only Agent and opens the system browser.
3. Sign in to SupDance in that browser if needed.
4. Ask WorkBuddy to check the connection and read the current canvas. Acceptance requires `canvas_connection_status` to return `hasCanvas=true` and `canvas_get_state` to return the live title and nodes.

The browser pairing link is single-use and lasts 60 seconds. The Agent's long-lived token stays in its protected local configuration and is not included in the connector package. Local MCP configuration is separate from the website account session.

## Scope and data

This connector can read canvas state and selections, modify nodes and prompt flows, and submit image-generation requests only when the user explicitly asks. Generation is asynchronous; a successful tool response does not prove an image is finished or credits were settled. The website and user account determine current model availability and pricing.

See [Privacy](PRIVACY.md), the [SupDance privacy policy](https://www.supdance.com/privacy), and [terms](https://www.supdance.com/terms). Troubleshooting is in [TROUBLESHOOTING.md](TROUBLESHOOTING.md). Support: https://github.com/Blacklake-Go/supdance-canvas-workbuddy/issues.

## Release gates

- Agent v0.1.7 source and fixed WorkBuddy tarball are published at the linked public GitHub release; clean-cache npx installation and MCP initialization/tools/list succeeded with 36 server tools. The package entry point disables Codex conversation restoration without relying on client environment-variable propagation.
- Install connector version 0.1.5 in the WorkBuddy desktop app and verify it filters the five disabled tools, invokes canvas_open, reports hasCanvas=true, and reads the current live canvas.
- Verify analysis, node editing, reconnection, and one explicitly authorized image-generation task against real website records.
- Confirm the connector source ID is available, review the market metadata and package contents, then submit the zip to the WorkBuddy team for review.
- Report “submitted for review” until the public marketplace entry is searchable and installable.

WorkBuddy connector requirements: https://open.workbuddy.cn/docs/connector.
