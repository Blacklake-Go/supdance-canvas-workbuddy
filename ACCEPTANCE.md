# Acceptance record

Checked: 2026-10-18 (Asia/Taipei)

## Source and package provenance

- WorkBuddy connector source: https://github.com/Blacklake-Go/supdance-canvas-workbuddy
- Connector version/source: `0.1.5` / `supdance-canvas-workbuddy`
- Shared Agent source: https://github.com/Blacklake-Go/supdance-canvas-agent
- WorkBuddy Agent release: `v0.1.7`, source commit `cc6bc837796673d93b8a56ed6aa94becab4d7a1c`
- Fixed Agent release asset: https://github.com/Blacklake-Go/supdance-canvas-agent/releases/download/v0.1.7/supdance-canvas-agent-workbuddy-0.1.7.tgz
- Agent asset SHA-256: `ecacb97a5eb495e143b0b533d2768dc7265927b872dc44ca849aa4a1ea1e9b0f`
- Rebuilt connector review archive: https://github.com/Blacklake-Go/supdance-canvas-workbuddy/releases/download/v0.1.5/supdance-canvas-workbuddy-0.1.5.zip
- Rebuilt connector archive SHA-256: `75a479a326ec8a3f06badd0430438b051f9f15f44d9ae55c741d7a1983e71953`
- The rebuilt archive passed `unzip -t` and contains connector metadata, one MCP server config, icon, Skill, README, changelog, privacy, troubleshooting, and notice files. The earlier upload ZIP is no longer present locally, so this rebuilt archive has not been proven byte-for-byte identical to the ZIP attached to the portal submission.

The installed Codex plugin is cached at `~/.codex/plugins/cache/supdance-local/supdance-canvas/0.1.1`; its `mcp.json` starts `supdance-canvas-agent mcp`. The matching Codex source is https://github.com/Blacklake-Go/supdance-canvas-codex, whose current `main` commit is `bb9bdd90f6b0a067a7c9f673e702246ad44dbe37`. The WorkBuddy connector is maintained in its own repository; both clients reuse the separate shared Agent source.

## Runtime path

WorkBuddy loads the single `stdio` MCP server with its managed Node 20 runtime. `npx` downloads the fixed Agent `v0.1.7` GitHub release tarball and starts `supdance-canvas-agent-workbuddy mcp`. The MCP process starts or reuses the local Agent on loopback. `canvas_open` creates a short-lived launch ticket and opens the system browser; the signed-in SupDance Canvas page pairs with the Agent, then sends current canvas state and tool results over the local authenticated bridge. The browser carries the website session; the package includes no account credential or Agent token. The Agent source binds to loopback and tests one-use, 60-second SSE tickets with origin/client binding.

## Verification

| Gate | Result | Evidence and limits |
| --- | --- | --- |
| Connector structure and metadata | Pass | One stdio MCP server; fixed Agent release; Node runtime 20; `staticEnv` bypasses local proxy; source uses kebab-case; bilingual names, descriptions and three examples per language; minimum WorkBuddy 5.0.0; icon is PNG 64×64. Official connector guide: https://open.workbuddy.cn/docs/connector. |
| Agent build and tests | Pass | `npm test`: 135 passed, 0 failed. |
| Fixed WorkBuddy Agent package | Pass | Downloaded release asset hash matches GitHub release digest. Clean-cache package check passed MCP initialize, found 36 tools, verified required canvas tools, and confirmed Codex conversation restoration is disabled in the WorkBuddy entry point. The isolated check correctly reported no connected browser. |
| WorkBuddy desktop startup and tool calls | Partial pass | In WorkBuddy 5.8.4, a connector task invoked `canvas_open`, `canvas_connection_status`, and `canvas_get_state`. It recovered after the Agent was initially unavailable and reported `agentRunning=true`, Agent `0.1.7`, `hasCanvas=true`; WorkBuddy read the source image node as a 1254×1254 PNG. This proves a live WorkBuddy session, not a clean-market install. The local Agent was no longer listening on port 17372 after the long-running task was cancelled, so it is not currently running. |
| MCP tool discovery in WorkBuddy | Partial pass | The fixed package's stdio MCP discovery returned 36 tools. WorkBuddy then invoked canvas tools successfully. A fresh clean-install flow from the market is still unverified because the connector is under review. |
| Canvas connection and read | Pass for the observed session | WorkBuddy's live call reached the signed-in canvas and read its source image. A current connected canvas snapshot from the companion local bridge reported `hasCanvas=true`, title `无限画布 1`, 11 nodes, 10 connections, and one selected image node. The later `canvas_get_selection` call through that companion bridge returned `fetch failed`; separate selection-tool behavior in a clean WorkBuddy session remains unverified. |
| Content analysis | Partial pass | WorkBuddy identified the selected white snake logo and correctly described its 1254×1254 PNG source. Broader prompt/node analysis coverage has not been measured. |
| Node and prompt workflow writes | Partial | The WorkBuddy task created text/config generation-flow nodes and connections. Re-reading showed the configurations stayed `idle`; one prompt composition included an unexpected `hhh` suffix, and the second prompt retained node-reference markup. No completed generation flow was verified. |
| Real image generation | Not passed | The single authorized task `image-1` was submitted for Seedream 4.7, 1:1, one image. It remained `queued` with no output and no status update. The current workbench model list exposes only `gpt-image-2`, even though the form's current value shows `seedream-4.7`. No replacement model or second generation was submitted. |
| Credit settlement | Unverified | No generated asset or account ledger entry was obtained. Do not report a debit or a zero-cost result without the website's credit record. |
| Recovery scenarios | Partial | Automated tests cover launch, local Agent identity, origin/client binding, one-use 60-second tickets, and restart-related logic. A WorkBuddy `canvas_open` recovered the observed session once. Browser-close/reopen, Agent restart, expired pairing ticket, and expired SupDance login were not all exercised in WorkBuddy 5.8.4. |
| macOS | Partial | WorkBuddy 5.8.4 and macOS were used for the live session and clean package check. Windows/Linux have not been tested. |
| Official WorkBuddy review | Submitted; review pending | The developer portal connector list shows `SupDance 画布`, version `0.1.5`, ID `oc_9d39174528d01e6f`, status `审核中`. No public-market search/install check has passed; do not call it listed or published yet. |

## Remaining acceptance work

1. Recheck the same generation task ID and the account's credit ledger. Do not retry or change models without a new user instruction.
2. Install from a clean WorkBuddy state after the marketplace review permits it, confirm the MCP tools, and rerun connection/read/selection checks.
3. Verify a safe text-node write and its read-back in WorkBuddy; fix and retest the prompt-flow serialization issue before claiming prompt workflows pass.
4. Exercise browser/Agent restart and ticket-expiry recovery, and test Windows/Linux before making cross-platform claims.
5. Recheck the official connector status. Report “listed” only after it is searchable and installable from the public marketplace.
