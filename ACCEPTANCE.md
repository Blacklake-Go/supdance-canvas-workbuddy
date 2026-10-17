# Acceptance record

Current connector candidate: 0.1.3
WorkBuddy client: macOS 5.8.4
Agent source: https://github.com/Blacklake-Go/supdance-canvas-agent
Agent source commit: c282cacde83d29e4416c15d1f23c694a11f69429
Agent tag: v0.1.5
Agent WorkBuddy tarball:
https://github.com/Blacklake-Go/supdance-canvas-agent/releases/download/v0.1.5/supdance-canvas-agent-workbuddy-0.1.5.tgz

| Gate | Result | Evidence |
| --- | --- | --- |
| Agent build and unit/acceptance suite | Pass | npm run build; 134/134 tests pass. |
| Agent production dependency audit | Pass | npm audit --omit=dev: 0 vulnerabilities. |
| WorkBuddy package contents | Pass | Fixed 0.1.5 tarball is 96,811 bytes and includes npm-shrinkwrap.json. |
| Clean-cache MCP startup | Pass | npx against the local fixed tarball and the public GitHub Release URL completed MCP initialize and tools/list; server reports Agent 0.1.5 and 36 tools. |
| WorkBuddy desktop MCP installation and filtering | Pending | Must be verified in the signed-in WorkBuddy app. |
| Canvas browser pairing | Pending | Require hasCanvas=true from WorkBuddy MCP status. |
| Current canvas and selection reads | Pending | Record live title and node/selection counts after app install. |
| Canvas analysis | Pending | Verify analysis against live returned nodes. |
| Node write / prompt flow | Pending | Use a reversible test node or user-approved target and re-read the canvas. |
| Browser / Agent recovery | Pending | Test disconnect, browser reopen, Agent restart, ticket expiry, and login expiry. |
| Real image generation and credit settlement | Pending | Check current Seedream 4.7 price and account state; one image only if no more than 15 credits. Verify task, image, canvas node, and account debit. |
| macOS | Partial | WorkBuddy 5.8.4 and package installation tested; in-app connector path pending. |
| Windows / Linux | Not tested | No cross-platform claim. |
| WorkBuddy market source uniqueness | Pending | Confirm in official developer submission flow. |
| Official market review | Not submitted | Requires completed WorkBuddy app acceptance and package review. |

The clean-cache MCP test proves package installation and MCP discovery only. It
does not prove a WorkBuddy desktop connection, a live canvas session, node
editing, image generation, or credit settlement.
