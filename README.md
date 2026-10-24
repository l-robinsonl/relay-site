# relay-site

The marketing site for [Relay](https://github.com/l-robinsonl/relay), a
local-first desktop API client.

Two files and a stylesheet. No framework, no build step, no
dependencies — partly because the page is small enough not to need any,
and partly because a site arguing against shipping a browser to send an
HTTP request should not ship 200 KB of JavaScript to render six
paragraphs.

## Running it

Open `index.html`. That is the whole workflow.

For a local server, so relative links behave exactly as they will in
production:

```sh
python3 -m http.server 8000
```

## Deploying

It is static, so almost anywhere works with no configuration:

- **GitHub Pages** — Settings → Pages → deploy from `master`, root.
- **Render** — a Static Site, no build command, publish directory `.`.
- **Netlify, Cloudflare Pages, S3** — upload the directory.

## House rules

**Never publish a number this project has not measured.** The
comparison table comes from `scripts/measure-memory.sh` in the Relay
repository, run on one machine with both applications idle, and the
page says so. It quotes PSS rather than RSS because PSS divides shared
memory instead of counting it twice, which is the honest figure and
also the less flattering one.

**Keep the status section current.** The page tells people what is not
finished — unsigned builds, no hosted option — before they find out
themselves. That section is the reason the rest of the page is worth
believing. When something ships, move it; do not quietly delete it.

**The claims are checkable on purpose.** Every assertion about what
Relay does corresponds to something in the source. If a feature
changes, the page changes.

## Palette

Lifted from the application itself (`apps/desktop/src/styles/main.css`)
so the two read as one product. Dark is the default; light is the
override, matching the app.
