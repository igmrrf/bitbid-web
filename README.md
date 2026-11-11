# bitbid landing page

Static HTML/CSS/JavaScript landing page in
[igmrrf/bitbid-web](https://github.com/igmrrf/bitbid-web), with production branch
`main`. The Yew browser console lives in
[igmrrf/bitbid-webapp](https://github.com/igmrrf/bitbid-webapp); the native CLI and
shared Rust core live in [igmrrf/bitbid](https://github.com/igmrrf/bitbid).
The previous `bitbid` repository's `web/main` branch retains the shared-origin
history; existing local checkouts keep that remote as `shared`.

## Cloudflare Workers

Use the existing **bitbid-web** Worker and connect this repository with these
Workers Builds settings:

| Setting | Value |
| --- | --- |
| Production branch | `main` |
| Root directory | `/` (repository root) |
| Build command | `exit 0` |
| Deploy command | `npx wrangler deploy` |

Wrangler reads the checked-in `wrangler.jsonc`. Its assets-only configuration
serves this directory without a Worker JavaScript entry point. The positive
allowlist in `.assetsignore` uploads only `index.html`, `app.js`, `styles.css`
and the four public font files. Git metadata, configuration, documentation,
caches and private files are excluded. Add any new public file to that allowlist
explicitly. Workers Builds has no Pages-style build output directory setting:
the Wrangler asset directory and allowlist select the files.

If the dashboard reports a disconnected Git account, reconnect the authorized
Git integration before expecting pushes to trigger builds. Repository changes
do not repair that connection. Connecting Git and deploying the existing Worker
are separate account actions; this repository does not provision them.

No frontend build step, runtime environment variable, secret, D1 binding or
backend service is required. Wrangler packages the HTML, CSS, JavaScript and
fonts directly from this repository.

Validate and preview a fresh clone locally from its root, for example:

```sh
git clone https://github.com/igmrrf/bitbid-web.git
cd bitbid-web
npx wrangler deploy --dry-run
npx wrangler dev --local --ip 127.0.0.1 --port 8081
```

The dry run validates packaging without deploying. Local preview uses the same
asset configuration and allowlist as deployment.
Use a current Wrangler runtime that supports the configured compatibility date
(`2026-11-11`); older bundled runtimes can reject local startup.

The source preserves the existing visual design and assets. It remains a static
landing page; these hosting settings do not activate the planned production
backend.

## Alternative: Cloudflare Pages

For a separately chosen Pages project, use branch `main`, framework `None`,
repository root, Build command `exit 0`, and Build output directory `.`. The
Workers `.assetsignore` allowlist is specific to Wrangler; prepare an equivalent
public-only output directory before using Pages. These Pages fields do not
configure the existing Worker.
