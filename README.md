# Rahlah — Customer app

A static single-page app (`index.html`) for booking a shared or private seat on the
Rahlah shuttle. Talks to the [rahlah-backend](../rahlah-backend) API over HTTP + WebSocket
— this repo has no server of its own.

## Before deploying

Open `index.html`, find this block near the top of the `<script>` tag, and set it to your
deployed backend's URL:

```js
const CONFIGURED_API_BASE = ''; // e.g. 'https://rahlah-backend.onrender.com'
```

Leave it blank for local testing — it falls back to `http://localhost:3000`.

## Run it locally

No build step, no dependencies. Any static file server works:

```bash
npx serve .
```

Or just open `index.html` directly in a browser, as long as the backend is running and
`CONFIGURED_API_BASE` points at it (opening via `file://` can be flaky with fetch/WebSocket
in some browsers — `npx serve .` is more reliable).

## Deploying to Render

`render.yaml` is set up as a **Static Site** Blueprint — no build step needed, since this
is plain HTML/JS. On Render: **New → Blueprint**, point it at this repo. Static sites on
Render are free and don't spin down (unlike free web services), so this is the cheapest
and most reliable piece of the whole stack to host.

Make sure `CONFIGURED_API_BASE` is set to your backend's live URL *before* you commit and
deploy — there's no environment-variable override for a static site, since there's no
server-side process to read one.
