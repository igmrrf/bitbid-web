# bitbid landing page

Static HTML/CSS/JavaScript landing page in
[igmrrf/bitbid-web](https://github.com/igmrrf/bitbid-web), with production branch
`main`. The Yew browser console lives in
[igmrrf/bitbid-webapp](https://github.com/igmrrf/bitbid-webapp); the native CLI and
shared Rust core live in [igmrrf/bitbid](https://github.com/igmrrf/bitbid).
The previous `bitbid` repository's `web/main` branch retains the shared-origin
history; existing local checkouts keep that remote as `shared`.

## Cloudflare Pages

Connect this repository with these settings:

| Setting | Value |
| --- | --- |
| Production branch | `main` |
| Framework preset | `None` |
| Root directory | Leave blank (repository root) |
| Build command | `exit 0` |
| Build output directory | `.` |

No build tool, package manager, environment variable, secret, D1 binding or
backend service is required. The HTML, CSS, JavaScript and fonts are served
directly from this repository. Connecting and deploying the Pages project is a
separate account action; this repository does not provision it.

Serve a fresh clone locally from its root, for example:

```sh
git clone https://github.com/igmrrf/bitbid-web.git
cd bitbid-web
python3 -m http.server 8081 --bind 127.0.0.1
```

The source preserves the existing visual design and assets. It remains a static
landing page; these hosting settings do not activate the planned production
backend.
