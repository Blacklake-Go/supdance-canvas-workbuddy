# Privacy and data handling

The connector runs its MCP process and SupDance Canvas Agent on the user's
computer. Its HTTP service is bound to loopback and uses a locally stored
long-lived Agent token. Browser pairing uses a short-lived, single-use ticket.
The connector package contains no account credential or Agent token.

When the user asks the connector to read or modify a canvas, canvas data is
read from or sent to the SupDance Canvas page already open in that user's
browser. WorkBuddy may include relevant tool inputs and outputs in its own
conversation history according to the user's WorkBuddy settings.

If the user explicitly requests image generation, the request is submitted
through the SupDance website using the signed-in account. The selected model
provider receives the prompt, required reference material, and generation
parameters. SupDance credits may be charged under the current account pricing.
The connector does not send a generation request while merely preparing a
prompt flow.

Review SupDance's current [privacy policy](https://www.supdance.com/privacy)
and [terms of service](https://www.supdance.com/terms) for service-side
retention and processing details. This connector does not make a separate
retention promise.
