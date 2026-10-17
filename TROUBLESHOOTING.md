# Troubleshooting

## WorkBuddy reports that the local Agent is unavailable

Call `canvas_open` to start or reuse the Agent and open the recent canvas in
the system browser. Wait for the page to load, then call
`canvas_connection_status` and `canvas_get_state`. A connection is confirmed
only when status reports `hasCanvas=true` and state returns the live canvas.

## The Agent is running but no canvas is connected

Keep the browser page open at `https://canvas.supdance.com/canvas`. Sign in to
SupDance in that browser if needed, then call `canvas_open` again. Pairing
tickets expire after 60 seconds and can only be used once; opening again
creates a fresh ticket.

## The browser or Agent was restarted

Call `canvas_connection_status`. If `hasCanvas` is false, call
`canvas_open`, keep the browser page open, and read state again after the page
reconnects. The local MCP process and browser Agent share the protected local
Agent configuration; do not copy its token into chat or connector settings.

## A canvas operation fails

Check that the requested node exists in the latest `canvas_get_state`
response and that the operation parameters match that node. Retry only after
checking the current state so a delayed response is not duplicated.

## An image-generation request is pending or failed

Use `generation_get_status` with the returned task identifier. A successful
submission response does not prove that an image completed or that credits
were charged. Check the visible task result and SupDance account records.
