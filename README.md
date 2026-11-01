# rehanzo.github.io

Static landing page for [rehanzo.com](https://rehanzo.com), hosted on GitHub Pages
behind Cloudflare. There are no application dependencies, JavaScript, or build step.

## Local preview

```sh
python3 -m http.server 8000 --bind 127.0.0.1
```

Open http://127.0.0.1:8000 and verify the styling and both links after changes.

## Security

The Content Security Policy in `index.html` must stay before resource-loading
markup. It allows local stylesheets and blocks scripts (including inline handlers),
other resource types, form submissions, and changes to the document's base URL.
The referrer policy prevents outgoing links from sending a `Referer` header.
Revisit the policy deliberately before adding images, fonts, or other resources.

Cloudflare currently redirects public HTTP traffic to HTTPS. GitHub Pages's origin
HTTPS-enforcement setting is separate; coordinate it with Cloudflare's SSL/TLS mode
before changing it.

Meta CSP cannot enforce `frame-ancestors`. To prevent other sites from framing this
page, configure a `Content-Security-Policy: frame-ancestors 'none'` response header
at Cloudflare. `X-Content-Type-Options: nosniff` and HSTS also require real HTTP
response headers; adding them as HTML meta tags does not enforce those protections.
See the [CSP meta delivery limitations](https://www.w3.org/TR/CSP3/#meta-element).

## Deployment

GitHub Pages publishes the repository root from `master`; no repository-defined
GitHub Actions deployment workflow is needed. Keep `CNAME` set to `rehanzo.com`.
After reviewing and committing changes, `git push origin master` publishes them.
