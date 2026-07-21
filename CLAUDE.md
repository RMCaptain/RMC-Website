# CLAUDE.md — RMC Website Project

## Project Overview
Building a world-class custom HTML/CSS/JS marketing site for Rocky Mountain Co.
Hosted on Netlify. Domain managed via GoDaddy (rockymountainco.ca).
Currently live on Squarespace — this replaces it.

---

## Company: Rocky Mountain Co. (RMC)

**Tagline:** "We obsess over Amazon, so you don't have to."

**What they do:** Full-service Amazon growth partner for established e-commerce brands.
- Buy: Strategic brand analysis, direct inventory purchasing, logistics from own facilities
- Optimize: Content, listing enhancement, Amazon SEO
- Grow: Custom ad campaigns, Vine, A+ Content, Storefronts
- Scale: Full ops management — customer service, returns, product launches, ad management

**Target clients:** E-commerce brand founders and marketing/ops leads at brands doing $5M–$50M revenue. CPG, health, beauty, grocery. They need a strategic partner, not a freelancer.

**Proof point:** Case studies showing brands scaled from $2K → $200K/month in 32 months.

**Location:** Edmonton, AB
**Contact:** (825) 462-1035 | info@rockymountainco.ca

---

## Brand Voice & Tone

- Professional, direct, confident — not hype
- Data-driven language
- Operator tone, not marketer tone
- No fluff, no corporate-speak
- Short sentences, clear benefit statements

---

## Owner

**Mike Sieben** — CEO/Founder
- Strengths: sales, strategy, simplifying complex models
- Hates: bloated systems, long copy, vague positioning
- Wants: clean, fast, high-converting site that builds credibility

---

## Site Goals

1. Build trust and authority immediately
2. Communicate the model simply (Buy → Optimize → Grow → Scale)
3. Drive inbound inquiries (primary CTA)
4. Showcase proof (case studies, results)

---

## Deploy — IMPORTANT

Pushing to GitHub does NOT deploy. The live site ships via Netlify CLI from local disk:

```powershell
# Deploy ONLY committed state (never a dirty working tree — a manual deploy ships everything on disk):
git worktree add --detach "$env:TEMP\rmc-site-deploy" master
# The CEO video is untracked (too large for git) — copy it in or the site 404s it:
Copy-Item "Mike - Video.mp4" "$env:TEMP\rmc-site-deploy\Mike - Video.mp4"
# Strip internal files — everything in the deploy dir becomes publicly served:
Remove-Item "$env:TEMP\rmc-site-deploy\CLAUDE.md", "$env:TEMP\rmc-site-deploy\.gitignore" -Force
Remove-Item "$env:TEMP\rmc-site-deploy\.netlify" -Recurse -Force
netlify deploy --prod --dir "$env:TEMP\rmc-site-deploy" --site e2d42b71-f9e1-4d98-9f82-e55b5777bb1f
git worktree remove "$env:TEMP\rmc-site-deploy" --force
```

After deploying, verify: home page hero (`heroCanvas` in source), `/Mike%20-%20Video.mp4` returns 200, `/CLAUDE.md` returns 404.

**History (2026-07-21):** the 2026-07-16 deploy reverted the home page because the particle-hero
index.html had sat uncommitted since May — the worktree deploy shipped the stale committed version
and dropped the untracked video. Commit before deploying; the working tree must be clean.

Netlify login: mike@rockymountainco.ca (already authed on this machine). Site: jovial-alfajores-475c9d → rockymountainco.ca. Commit before deploying; never deploy with uncommitted work in the folder.

## Build Rules

- Mobile-first, fast-loading
- Clean modern design — no stock photo clutter
- Tailwind CSS preferred (via CDN) or clean custom CSS
- Vanilla JS only — no heavy frameworks
- Netlify-ready static files (index.html + assets)
- No CMS needed initially — content is baked in
- Accessible, semantic HTML
