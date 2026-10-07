# Crawler & recruiter traffic: what was added and how to check it

Maintenance notes for the crawler/recruiter layer of https://ztxtech.github.io/.
This file lives in `docs/`, which is excluded from the Jekyll build, so it is never
published.

## What was added

| File | Purpose |
| --- | --- |
| `robots.txt` | Explicitly allows search engines and AI/LLM crawlers, links `sitemap.xml`. Replaces the one-line file that `jekyll-sitemap` generated. |
| `llms.txt` | Plain-text profile written for AI assistants and recruiting tools: expertise, selected work, experience, availability, contact. Openly published, not hidden. |
| `_includes/head/structured-data.html` | `ProfilePage` + `Person` JSON-LD (`knowsAbout`, `alumniOf`, `affiliation`, `sameAs`, `seeks`). |
| `_includes/seo.html` | Real `<title>`, `meta description`, keywords, robots directives, canonical, Open Graph and Twitter cards. |
| `_includes/attribution.html` | First-touch channel capture, GA4 `first_touch` / `contact_click` events, channel tag in `mailto:` subjects. |
| `_config.yml` | `url`/`baseurl` so canonical and sitemap URLs are absolute; `seo:` and `profile:` copy blocks; `_pages/includes` excluded from the build. |

## Where the facts live

- Visible copy: `_pages/includes/*.md`
- Machine-readable profile (JSON-LD): `profile:` block in `_config.yml`
- Machine-readable summary (plain text): `llms.txt`

`llms.txt` is a static file, so it is not generated from `_config.yml`. When you change
one, update the other, then bump `profile.updated` in `_config.yml`.

## Knowing where a visitor came from

Three layers, none of them server-side (GitHub Pages serves static files only):

1. **GA4** (`G-WE2J7LBCGB`): `first_touch` event carries channel, medium, campaign,
   landing page and referrer host. `contact_click` fires when someone clicks an email
   link, so you can see which channel produces real inquiries.
2. **Channel links**: share `https://ztxtech.github.io/?ref=linkedin`,
   `?ref=wechat`, `?ref=cv`, `?ref=conference`, etc. The first touch wins, so the
   channel is remembered even if the visitor returns later directly.
3. **Email subject**: `mailto:` links are rewritten to
   `Research inquiry for Tianxiang Zhan (via <channel>)`, so the first email you receive
   already tells you which channel the person came from. Delete the `tagEmailLinks`
   block in `_includes/attribution.html` if you dislike the subject line.

### Crawler traffic

GitHub Pages does not expose access logs, so bot hits (GPTBot, ClaudeBot, Googlebot)
are invisible in GA4. To actually see them, put Cloudflare (free plan) in front of the
site; its HTTP request log and AI Crawl Control show which crawler fetched which path,
so you can verify that `/llms.txt` and `/` were read.

Search-side diagnostics: Google Search Console and Bing Webmaster Tools show queries,
impressions and indexed URLs; both support the verification tags already wired into
`_includes/seo.html` (`google_site_verification`, `bing_site_verification`).

## Deliberately not implemented

Covert instructions aimed at AI agents, and canary markers such as an intentional
typo used to detect that a model read hidden text. Hidden text is cloaking under
search engine spam policies and prompt injection under most AI vendors' usage policies,
both of which put the whole site at risk. Everything here is readable by humans and
machines alike.
