---
title: "Growing My Website: Analytics, Comments, and Google Search Console"
date: 2026-07-02 21:30:00 +08:00
categories:
  - meta
tags:
  - github-pages
  - chirpy
  - goatcounter
  - giscus
  - google-search-console
  - website
toc: false
---

After publishing my [first blog post](/posts/building-this-website-from-scratch/), the website finally existed — but it still felt a little quiet.

I could open the site myself, but I had no idea whether anyone else had visited. Readers had no way to leave comments. And if someone searched my name or this site on Google, would anything show up at all?

So I spent the next few days adding three things:

- **GoatCounter** for page view analytics
- **Giscus** for blog comments
- **Google Search Console** so Google knows the site exists

This post is a record of how I did it — and the pitfalls I ran into along the way.

---

## Why These Three?

They solve three different problems:

| Tool | What it does |
|------|----------------|
| **GoatCounter** | Tells me how many people visit each page |
| **Giscus** | Lets readers comment using their GitHub account |
| **Google Search Console** | Helps Google discover and index my pages |

They are independent. I can use all three at the same time without conflict.

---

## Part 1: GoatCounter Analytics

Chirpy supports several analytics providers, but if you want **page view counts displayed on each post**, GoatCounter is currently the only built-in option.

### Setup steps

1. Register at [goatcounter.com](https://www.goatcounter.com/)
2. Create a site (mine is `universe-ustc`)
3. Add two lines to `_config.yml`:

```yaml
analytics:
  goatcounter:
    id: universe-ustc

pageviews:
  provider: goatcounter
```

4. Push and wait for deployment

![GoatCounter dashboard after registration](/assets/img/posts/goatcounter-dashboard.png)

After deployment, each blog post should show a view count near the author line, and the GoatCounter dashboard will start recording visits.

### A small note

If you use an ad blocker, it may block `gc.zgo.at`. If your own visits do not show up, try disabling the blocker or opening the site in a private window.

---

## Part 2: Giscus Comments

I chose [Giscus](https://giscus.app/) because it is free, privacy-friendly, and integrates naturally with GitHub.

### Setup steps

1. Enable **Discussions** in the GitHub repository settings
2. Go to [giscus.app](https://giscus.app/) and connect the repository
3. Choose a discussion category (I used `General`)
4. Set the mapping to **pathname** (one discussion thread per blog post)
5. Copy the generated configuration values into `_config.yml`:

```yaml
comments:
  provider: giscus
  giscus:
    repo: Universe-ustc/Universe-ustc.github.io
    repo_id: R_kgDOTJkRXQ
    category: General
    category_id: DIC_kwDOTJkRXc4DAUvI
    mapping: pathname
    strict: "0"
    input_position: bottom
    lang: en
    reactions_enabled: "1"
```

6. Make sure individual posts do **not** have `comments: false` in their front matter

![Giscus configuration page](/assets/img/posts/giscus-setup.png)

![Giscus generated script and parameters](/assets/img/posts/giscus-script.png)

### Important: you do not paste the `<script>` tag yourself

Giscus.app will show you a `<script>` snippet at the bottom. **Do not paste it into your HTML.**

Chirpy injects Giscus automatically once `comments.provider` is set to `giscus`. You only need the YAML configuration.

---

## Part 3: Google Search Console

Having a live website does not mean Google already knows about it. Search Console is how you tell Google: this site exists, please come index it.

### Verification

Google offered several verification methods. I used the **HTML file** method:

1. Download `google46bb380d05484c3d.html`
2. Place it in the **root** of the repository
3. Push to GitHub
4. Confirm the file is accessible at `https://universe-ustc.github.io/google46bb380d05484c3d.html`
5. Click **Verify** in Search Console

![Google Search Console HTML file verification](/assets/img/posts/gsc-verification.png)

**Do not delete this file after verification.** Google requires it to stay on your site.

### Requesting indexing

After verification, I used **URL Inspection** to request indexing for important pages.

At first, only the homepage passed inspection. Subpages like `/about/` and `/blog/` showed:

> URL is not on Google

![Google Search Console URL not indexed yet](/assets/img/posts/gsc-url-not-indexed.png)

This is normal for a brand-new site. Google discovers the homepage first; other pages take time. You can speed things up by clicking **Request Indexing** on each important URL.

---

## Pitfalls I Hit Along the Way

### 1. The site looked unchanged after pushing

I pushed updates, but my browser still showed the old layout — old sidebar, old home page, everything.

**Cause:** Chirpy enables **PWA offline caching** by default. Your browser may serve a cached version of the site.

**Fix:** Hard refresh with `Ctrl + Shift + R`, or clear site data in DevTools → Application.

![Old site layout still showing due to PWA cache](/assets/img/posts/pwa-cache-old-layout.png)

### 2. Local changes were not actually deployed

Several times I thought I had fixed something, but the live site still showed the old content.

**Cause:** I edited files locally but forgot to `git commit` and `git push` — or the push failed due to network issues.

**Fix:** Always run `git status` and confirm the push succeeded. On unstable networks, this worked for me:

```powershell
git -c http.version=HTTP/1.1 push
```

### 3. About page Markdown did not render

My About page showed raw text like `## About Me` and `**bold**` instead of formatted HTML.

**Cause:** Markdown was nested inside HTML `<div>` blocks. Jekyll/Kramdown does not parse Markdown inside HTML unless you add `markdown="1"` — and nested blocks are still tricky.

**Fix:** Keep Markdown **outside** HTML wrappers. Use HTML only for special layout pieces like the education timeline.

### 4. Custom CSS did not apply to all pages

Heading colors only changed on the Home page.

**Cause:** I put `custom.css` in `_includes/head/custom.html`, but Chirpy actually loads custom head content from **`_includes/metadata-hook.html`**.

**Fix:** Move the stylesheet link to `metadata-hook.html`.

### 5. Giscus and GoatCounter are not the same as Google indexing

GoatCounter recording a visit does **not** mean Google has indexed the page. Search Console verification does **not** mean you will appear in search results immediately.

These are three separate systems. Each one needs its own setup and patience.

---

## What Is Working Now

- Page view counts on blog posts (GoatCounter)
- Comment section at the bottom of posts (Giscus)
- Google Search Console verification completed
- Homepage URL inspection looks good; other pages are queued for indexing

There is still plenty to improve — more content, better SEO, a Google Scholar profile — but the site feels more like a real website now, not just a static page I visit alone.

---

## Closing Thoughts

Compared to the first post, this stage felt less dramatic. No green checkmark anxiety from GitHub Actions (well, mostly). Just a series of small integrations, each with its own documentation, configuration file, and ways to go wrong.

If you are building a Chirpy site on GitHub Pages, I hope these notes save you an hour of confusion — especially the PWA cache issue, which fooled me more than once.

More posts coming soon.
