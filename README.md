# Synapse Client

Google Tag Manager server-side client template that receives the events of the
[Synapse Tag](https://github.com/synapse-marketing/synapse-tag) and of
server-to-server senders (for example offline purchases on an extra path such
as /webhook) and turns them into event data for the server tags.

- Pixels, POST requests with JSON or form bodies, several events per request.
- A client id kept in the `_dcid` cookie, the `synapse` cookie of the tag
  extended, the GA4 FPID cookie copied for the browser when needed, all subject
  to the cookie consent settings.
- What the Synapse Tag keeps in its `synapse` cookie (rows set to Store) is
  added to every event that lacks it, when the visitor allowed advertising
  (`consent_state` from the Synapse Tag: `ad_storage` granted and
  `ad_user_data` not denied). A value the event has is never replaced.
- Response status, body and redirects.
- Every answer carries the client's own name (as set in the container) in the
  `x-synapse-client` header and the names of the events it received in the
  `x-synapse-event` header, so the Synapse logs show both as they are, on
  whatever path the request came.
- The disguised retry of the Synapse Tag is understood without an edge worker.

Import `template.tpl` in GTM: Templates, Client Templates, New, menu, Import.

Copyright 2026 Synapse. Apache License 2.0, see [LICENSE](LICENSE).
