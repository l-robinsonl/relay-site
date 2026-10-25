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

**Keep the status current.** The page tells people what is not
finished — unsigned builds, chiefly — before they find out themselves.
That honesty is the reason the rest of the page is worth believing.
When something ships, move it; do not quietly delete it.

**Every price must match the server.** The four figures on the page
come from the Stripe prices the sync server is configured with, and
the thousand included assistant messages from `RELAY_ASSISTANT_TURNS`,
which defaults to 1000. A page quoting a price the checkout does not
charge is worse than a page with no prices on it.

**Never call an assistant turn a "request".** On a page about an API
client, "1,000 requests a month" reads as a cap on the HTTP requests
Relay sends, which would be absurd — those are never counted. It is
also not a thousand questions: the server counts one per round trip to
the model, so a question that uses tools spends several. The page says
"messages to the model" and spells the distinction out.

**The free tier is load-bearing, not a funnel trick.** One person on
the hosted server is free forever with nothing held back, and
self-hosting is free for any number of people. Both are true in the
code — `Entitlement::solo()` and a server with no Stripe keys
configured — and the page says so plainly because that is the whole
argument for trusting the paid tier.

**Never invent a reason for a solo user to pay for sync.** The first
cut of this page had a Solo card and a Team card that were, for one
person, the same free thing, under a button reading "Start with one
person" — selling nothing. There are exactly two honest reasons to
charge: another person on a server that costs money to run, and model
requests that cost money per message. Anything else would mean holding
a feature back from the free tier, which contradicts the sentence
printed beside it and is the behaviour people are leaving Postman
over. The assistant is why a solo user might pay, and it is available
to one seat as readily as to ten.

**A feature grid may hold any number of cards.** The separator lines
are a ring on each card rather than a container background showing
through the gaps, so a row that does not fill simply ends. The old
version left a grey hole at any count that was not a multiple of the
column count, which changed with the viewport.

**The claims are checkable on purpose.** Every assertion about what
Relay does corresponds to something in the source. If a feature
changes, the page changes.

## Palette

Lifted from the application itself (`apps/desktop/src/styles/main.css`)
so the two read as one product. Dark is the default; light is the
override, matching the app.
