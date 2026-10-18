# Acceptance record

Checked: 2026-10-18 (Asia/Taipei)

## Latest recheck (2026-10-18 10:05 Asia/Taipei)

- The WorkBuddy Open Platform still shows `SupDance 画布` v0.1.5 submission `oc_9d39174528d01e6f` as `审核中`; the enterprise certification and developer information remain approved. It is not yet publicly listed.
- A fresh local runtime check used the exact WorkBuddy Agent package installed in the npx cache. MCP initialization exposed 36 tools, including `canvas_connection_status`, `canvas_open`, `canvas_get_state`, and `canvas_get_selection`. `canvas_open(mode=recent)` started Agent `0.1.7` and opened the signed-in SupDance canvas. The follow-up status and reads returned `agentRunning=true`, `hasCanvas=true`, title `无限画布 1`, 10 nodes, 8 connections, and no selected nodes. No canvas writes or media generation occurred.
- The current canvas snapshot contains four additional image nodes with `status=success`, one successful source image, two Seedream 4.5 edit nodes with `status=error` / `全部图片生成失败`, and a Seedream 4.7 image configuration node still `idle`. The four successful image nodes cannot be attributed to the earlier cancelled `image-1` task from available state, so they do not prove that task generated an image.
- The MCP status also reports `conversation.status=failed` with `Cannot find module '@openai/codex/package.json'` and `codexBusy=false`. The WorkBuddy canvas tools still succeeded; this is a separate Codex conversation subsystem error and should be resolved before claiming that conversation or Codex-driven generation paths work.
- A new WorkBuddy 5.8.4 task was prepared in the authorized empty test workspace, but the app kept its Send control disabled. Switching back to Office mode showed `Failed to execute 'removeChild' on 'Node': The node to be removed is not a child of this node.` Retry restored the input box, but the new task still could not be submitted. The earlier successful WorkBuddy session at 08:42 remains the direct desktop-client proof; this fresh check proves the fixed MCP package and local bridge, not a new WorkBuddy UI invocation.
- The single approved Seedream 4.7 attempt remains cancelled in WorkBuddy with no result. Its backend terminal state and SupDance credit settlement remain unknown. No second generation was submitted.

## Earlier recheck (2026-10-18 09:30 Asia/Taipei)

- The WorkBuddy Open Platform certification page shows the publisher as a verified enterprise subject. The notification center separately confirms that the developer information passed review at 08:39 on October 18.
- The connector list still shows `SupDance 画布`, version `0.1.5`, submission `oc_9d39174528d01e6f`, as `审核中`. It is submitted, not publicly listed or installable from the market yet.
- The WorkBuddy 5.8.4 task history contains a successful read-only session from 08:42: `canvas_open` started Agent `0.1.7`, `hasCanvas=true`, and the task read the current canvas and selection. This is session-specific evidence, not proof the service is currently running.
- Current local check: WorkBuddy's stdio MCP process (`npm exec supdance-canvas-agent-workbuddy mcp`) is present, but nothing is listening on `127.0.0.1:17372`; `/health` is unreachable. A fresh read-only prompt is drafted in WorkBuddy, but its Send control is disabled, so no fresh WorkBuddy run was submitted this recheck.
- The single approved Seedream 4.7 attempt appears in WorkBuddy as cancelled after 8m15s with no image output. The last known backend status was `queued`; a subsequent `generation_get_status(image-1)` call through the companion Codex-side SupDance MCP returned `fetch failed`, so it does not establish the backend task's terminal state. Final backend state and SupDance credit settlement remain unknown. Do not retry or report a debit/refund without a current task result and account ledger evidence.
- The official [WorkBuddy connector guide](https://open.workbuddy.cn/docs/connector) was rechecked. It still specifies MCP + Skill, one MCP Server, a fixed package and `minWorkbuddyVersion` for versioned fields, plus platform review before appearing in the public connector market.

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
| WorkBuddy desktop startup and tool calls | Partial pass | An earlier WorkBuddy 5.8.4 session directly invoked `canvas_open`, `canvas_connection_status`, and `canvas_get_state`, then read the source image node as a 1254×1254 PNG. The 10:05 recheck separately initialized the fixed WorkBuddy package and proved the local bridge read; it did not produce a fresh WorkBuddy UI task because Send stayed disabled. A clean-market install is still unverified while the connector is under review. |
| MCP tool discovery in WorkBuddy | Partial pass | The fixed package's stdio MCP discovery returned 36 tools, including all required connection and canvas read tools. WorkBuddy previously invoked canvas tools successfully. A fresh clean-install flow from the market is still unverified because the connector is under review. |
| Canvas connection and read | Pass for observed sessions | The earlier WorkBuddy session and the 10:05 fixed-package runtime check reached the signed-in canvas. The latest snapshot reported `hasCanvas=true`, title `无限画布 1`, 10 nodes, 8 connections, and no selected nodes; `canvas_get_selection` returned an empty selection. |
| Content analysis | Partial pass | WorkBuddy previously identified the selected white snake logo and correctly described its 1254×1254 PNG source. The latest read found four additional successful image nodes, two failed Seedream 4.5 nodes, and one idle Seedream 4.7 configuration node; those successful images cannot be tied to the cancelled `image-1` test, and visual post-generation analysis is not proven. |
| Node and prompt workflow writes | Partial | The WorkBuddy task created text/config generation-flow nodes and connections. Re-reading showed the configurations stayed `idle`; one prompt composition included an unexpected `hhh` suffix, and the second prompt retained node-reference markup. No completed generation flow was verified. |
| Real image generation | Not passed | The single authorized task `image-1` was submitted for Seedream 4.7, 1:1, one image. WorkBuddy later showed its assistant task as cancelled after 8m15s, with no output. The last known backend status was `queued`; the subsequent companion Codex-side status query returned `fetch failed`, so the backend terminal state is unknown. No replacement model or second generation was submitted. |
| Credit settlement | Unverified | No generated asset or account ledger entry was obtained, and the final backend task state could not be rechecked. Do not report a debit, refund, or zero-cost result without the website's credit record. |
| Recovery scenarios | Partial | Automated tests cover launch, local Agent identity, origin/client binding, one-use 60-second tickets, and restart-related logic. A WorkBuddy `canvas_open` recovered the observed session once. Browser-close/reopen, Agent restart, expired pairing ticket, and expired SupDance login were not all exercised in WorkBuddy 5.8.4. |
| macOS | Partial | WorkBuddy 5.8.4 and macOS were used for the live session and clean package check. Windows/Linux have not been tested. |
| Official WorkBuddy review | Submitted; review pending | The developer portal connector list shows `SupDance 画布`, version `0.1.5`, ID `oc_9d39174528d01e6f`, status `审核中`. The enterprise certification is complete and the developer information has passed review, but the connector itself has not. No public-market search/install check has passed; do not call it listed or published yet. |

## Remaining acceptance work

1. Restore a fresh WorkBuddy read-only task submission (the current draft's Send button was disabled), invoke `canvas_open`, and verify that the Agent starts and `hasCanvas=true`; check why the detached Agent is no longer listening after the prior task ended.
2. Recheck the same generation task ID and the account's credit ledger. Do not retry or change models without a new user instruction.
3. Install from a clean WorkBuddy state after the marketplace review permits it, confirm the MCP tools, and rerun connection/read/selection checks.
4. Verify a safe text-node write and its read-back in WorkBuddy; fix and retest the prompt-flow serialization issue before claiming prompt workflows pass.
5. Exercise browser/Agent restart and ticket-expiry recovery, and test Windows/Linux before making cross-platform claims.
6. Recheck the official connector status. Report “listed” only after it is searchable and installable from the public marketplace.
