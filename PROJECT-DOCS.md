# rohitthakur.in — Complete Project Documentation

**Status:** ✅ Live at https://rohitthakur.in  
**Last updated:** June 2026  
**Maintained by:** Rohit Thakur (rohitthakurin)

---

## Table of Contents

1. [Project Overview](#1-project-overview)
2. [Domain Portfolio](#2-domain-portfolio)
3. [Tech Stack & Architecture](#3-tech-stack--architecture)
4. [File Structure](#4-file-structure)
5. [Design System](#5-design-system)
6. [Site Sections — Content & Logic](#6-site-sections--content--logic)
7. [Skills & Capabilities](#7-skills--capabilities)
8. [Image Assets — How They Were Created](#8-image-assets--how-they-were-created)
9. [SEO & Schema](#9-seo--schema)
10. [Security Configuration](#10-security-configuration)
11. [GitHub Setup](#11-github-setup)
12. [Cloudflare Pages Deploy](#12-cloudflare-pages-deploy)
13. [DNS Configuration](#13-dns-configuration)
14. [YouTube RSS Video Feed](#14-youtube-rss-video-feed)
15. [How to Update the Site](#15-how-to-update-the-site)
16. [Pending / Future Work](#16-pending--future-work)
17. [Key Decisions & Rationale](#17-key-decisions--rationale)
18. [Social Profiles & Links](#18-social-profiles--links)

---

## 1. Project Overview

A personal professional hub for Rohit Kumar Thakur — Senior Manager & Head of IT at RightWave. The site serves as a single canonical destination that:

- Establishes professional credibility (infrastructure, security, 15+ years IT)
- Showcases real projects built and deployed from scratch
- Links out to YouTube channels (UtsavRaag, Vlogs by Rohit Thakur)
- Surfaces AI & automation skills alongside core IT expertise
- Displays RightWave's public recognition posts (Humans of RightWave, Employee Spotlight)

**Core principle:** Static, fast, no backend, no CMS, solo-maintainable.

---

## 2. Domain Portfolio

All three domains registered at **GoDaddy**, all nameservers pointed to **Cloudflare**.

| Domain | Purpose | Status |
|--------|---------|--------|
| `rohitthakur.in` | Primary personal hub | ✅ Live |
| `indiandalalstreets.in` | Trading YouTube brand | ⏳ Redirect pending |
| `thakuracademy.in` | Future teaching content | ⏳ Redirect pending |

**Hard rule:** Trading/market content must NEVER appear on rohitthakur.in. The indiandalalstreets brand is kept entirely separate for employer-identity and SEBI-adjacency reasons.

---

## 3. Tech Stack & Architecture

```
Stack:          Plain HTML + CSS + ~40 lines vanilla JS
Framework:      None
Build step:     None
Hosting:        Cloudflare Pages (free tier)
Repo:           github.com/rohitthakurin/rohitthakur.in
Deploy:         Auto-deploy on every git push to main
SSL:            Cloudflare Universal SSL (automatic, free)
CDN:            Cloudflare global network
Font:           Space Grotesk (Google Fonts)
JS deps:        None (vanilla only)
Video feed:     rss2json.com API (no API key needed)
```

**Why static?** No database, no PHP, no plugins to patch. Zero attack surface beyond the HTML itself. Updates are infrequent, so a CMS is unjustified complexity.

**Why Cloudflare Pages?** Free unlimited bandwidth, automatic HTTPS, global CDN, deploys from GitHub in ~30 seconds, no credit card required.

---

## 4. File Structure

```
rohitthakur.in/              (Dropbox/Rohit_Documents/rohitthakur.in/)
├── index.html               ← entire site (single page)
├── _headers                 ← Cloudflare security headers
├── _redirects               ← friendly URL aliases
├── robots.txt               ← allow all + sitemap reference
├── sitemap.xml              ← single URL sitemap
├── .gitignore               ← excludes .DS_Store files
└── assets/
    └── img/
        ├── rohit-portrait.webp    ← hero photo (26 KB, transparent bg)
        ├── og-card.png            ← social share card 1200×630
        ├── rw-featured.webp       ← Humans of RightWave post image
        └── rw-spotlight.webp      ← Employee Spotlight post image
```

---

## 5. Design System

```css
/* Colours */
--bg:       #0b0a14   /* near-black canvas */
--bg2:      #100e1c   /* slightly lighter for sections */
--panel:    rgba(255,255,255,.028)  /* glass cards */
--line:     rgba(255,255,255,.08)   /* borders */
--ink:      #edecf6   /* primary text */
--muted:    #9b9ab8   /* secondary text */
--faint:    #6c6b88   /* tertiary / disabled */
--violet:   #7c5cfc   /* primary accent */
--violet2:  #a855f7   /* gradient end */
--indigo:   #6366f1   /* button gradient */
--live:     #4ade80   /* green "live" badge */
--yt:       #ff4d4d   /* YouTube red */

/* Typography */
Display:  Space Grotesk (700/600) — headings
Body:     system-ui sans-serif — body text
Mono:     ui-monospace — code card, eyebrows, tags

/* Key sizes */
h1:       clamp(40px, 5.2vw, 64px)
h2:       clamp(27px, 4vw, 37px)
wrap:     max-width 1140px
```

**Animations:**
- Scroll reveal — IntersectionObserver, `opacity 0→1 + translateY 28px→0`
- Skill chips — staggered fade-in (55ms per chip) on scroll into view
- Hover — `translateY(-4px to -6px)` on cards
- Shimmer skeleton — on video cards while RSS loads
- `prefers-reduced-motion` — all animations disabled for accessibility

---

## 6. Site Sections — Content & Logic

### Navigation
Sticky, glassmorphism backdrop. Links: Home · About · Skills · Projects · Channels · Featured · Teaching (soon pill) + "Get in touch" CTA button.

Mobile: nav links hidden at ≤860px (hamburger not implemented — deliberate, keeps JS minimal).

### Hero
- Eyebrow: "infrastructure · security · maker"
- H1: "I keep systems **secure** & build for the web."
- Lead paragraph + role badge (Senior Manager · Server Admin @ RightWave)
- Two CTA buttons: "See my work →" / "My channels ▶"
- Right: photo in violet glow ring + floating code card (`rohit.js`)
- Photo: `rohit-portrait.webp` — background removed via Python/PIL/scipy pipeline, head-to-chest crop, bottom fade mask

### About
- Two-column: copy left, stats grid right
- Copy: full scope — 3-location infrastructure, IT Head, AI upskilling, personal interests (photography, old music, long drives, YouTube)
- Stats: 15+ years in IT · 24/7 uptime focus · 2 YouTube channels · Security first

### Skills
Six grouped chip groups (animated stagger on scroll):
1. **Infrastructure & servers** — Dell PowerEdge, VMware vSphere, Windows/Linux, MS SQL, MongoDB, MySQL, Redis, Tomcat, Apache/Nginx, Google Workspace, Email servers, Backup & DR, Zero-downtime migrations, Multi-location IT
2. **Email deliverability** — MX/SPF/DKIM/DMARC, Marketo, Pardot, HubSpot, IP blacklist monitoring, 99%+ delivery rates
3. **Network & security** — pfSense, Firewalls, ISO 27001/ISMS, Cyber security, SSL/TLS full lifecycle (CSR, JKS, DV/OV, Tomcat/IIS/XAMPP/WordPress/Linux, Let's Encrypt)
4. **AI & automation** — ChatGPT/Custom GPTs, Claude, Gemini, NotebookLM, n8n, Zapier, Make, Google Flow, Lovable
5. **Self-hosted platforms** — WordPress+Elementor, Hostinger, Rocket.Chat CE, Snipe-IT, Moodle LMS, TAO, Ubuntu Server, LAMP stack
6. **Cloud, web & domains** — Cloudflare, GoDaddy, Namecheap, DurableDNS, DNS management, HTML/CSS/JS, Git/GitHub, Static deployment

**Decision:** No % skill bars (credibility risk with technical audience). Chip groups are honest and extensible.

### Projects (6 real cards)
All self-deployed production systems:

| # | Project | Stack | Status |
|---|---------|-------|--------|
| 01 | Company Website (RightWave) | WordPress + Elementor, Linux → Hostinger | Live |
| 02 | Rocket.Chat CE | Ubuntu Server, self-hosted | Live |
| 03 | Snipe-IT Asset Management | Linux, self-hosted | Live |
| 04 | TAO Online Exam Platform | Linux VM, self-hosted | Live |
| 05 | Moodle LMS | Linux, self-hosted | Live |
| 06 | rohitthakur.in | HTML/CSS, Cloudflare Pages | Live |

### Channels
Two brand cards, each with YouTube + Instagram links:
- **UtsavRaag** — Devotional bhajans and festival music (Krishna, Shiv, Hanuman, Mata Rani)
  - YouTube: @UtsavRaag | Instagram: @utsavraag
- **Vlogs by Rohit Thakur** — Family vlogs, India road trips, street food, everyday moments
  - YouTube: @VlogsbyRohitThakur | Instagram: @vlogsbyrohitthakur

### Latest Videos
Auto-fetches 3 most recent videos (2 from UtsavRaag, 1 from Vlogs) on page load.
- Primary: `api.rss2json.com` (converts YouTube RSS to JSON)
- Fallback: `api.allorigins.win` (CORS proxy for raw XML)
- Shimmer skeleton shown while loading
- Each card: thumbnail → clicks to YouTube video (opens new tab, views count)
- **Important:** Only works on HTTPS. Does NOT work when opening `file://` locally.

### Featured (As seen on LinkedIn)
Two RightWave posts displayed as clickable images:

| Post | Year | Link |
|------|------|------|
| Humans of RightWave | 2025 | linkedin.com/posts/rightwave_humansofrightwave-...activity-7476290709885677568 |
| Employee Spotlight | 2023 | linkedin.com/posts/rightwave_employeespotlight-...activity-7168573717793521664 |

Images cropped from screenshots, optimised as WebP (~55-60 KB each).

**Note:** LinkedIn iframe embeds were tried and rejected — they show "Page not found" when visitor is not logged in. Static image approach is reliable for all visitors.

### Connect
- LinkedIn: /in/rohitthakur87
- GitHub: @rohitthakurin
- Email: mail2rohitthakur@gmail.com (mailto: link)

---

## 7. Skills & Capabilities

Full list for reference (also in GitHub README):

**Infrastructure & servers:** Server administration · Dell PowerEdge · VMware vSphere · Virtualization · Windows Server · Linux (Ubuntu/CentOS/Rocky) · Active Directory · MS SQL Server · MongoDB · MySQL · Redis · Apache Tomcat · Apache/Nginx · Google Workspace Admin · Email servers · Backup & DR · Zero-downtime migrations · Multi-location IT management

**Email deliverability:** MX/SPF/DKIM/DMARC · Email authentication & audits · Marketo · Pardot · HubSpot · IP & domain blacklist monitoring · 99%+ delivery rates

**Network & security:** pfSense firewall · Firewalls · Networking · ISO 27001/ISMS · Cyber security · SSL/TLS management · CSR generation · JKS (Java KeyStore) · Domain validation (DV/OV) · SSL on Apache Tomcat · SSL on IIS (ASP.NET) · SSL on XAMPP/WordPress (Linux) · Let's Encrypt (Certbot) · Certificate installation & renewal

**AI & automation:** ChatGPT & Custom GPTs · Claude (Anthropic) · Google Gemini · NotebookLM · n8n · Zapier · Make · Google Flow · Lovable · Prompt engineering

**Self-hosted platforms:** WordPress · Elementor · Hostinger · Rocket.Chat CE · Snipe-IT · Moodle LMS · TAO Exam Platform · Ubuntu Server · LAMP stack

**Web, cloud & domains:** HTML/CSS/JavaScript · Git & GitHub · Cloudflare · GoDaddy · Namecheap · DurableDNS · DNS management · Domain administration · Static site deployment

**Certifications:**
- AI and ChatGPT Workshop — Be10x (Mar 2026)
- AI Tools Workshop — Be10x (Feb 2026)
- VMware Certified Professional — Skillsoft (Jun 2023)
- Fundamentals of Information Security — Infosys Springboard (Jun 2023)
- Introduction to Cyber Security — Infosys Springboard (Jun 2023)

---

## 8. Image Assets — How They Were Created

### rohit-portrait.webp (26 KB)
- Source: Professional photo uploaded by Rohit
- Process: Python + PIL + scipy background removal pipeline
  - Border-connected white pixel removal (preserves white collar/buttons)
  - 2px edge dilation to remove JPEG fringe
  - Gaussian blur (0.8σ) for smooth edges
  - Cropped to head-and-chest (~63% height)
  - Bottom fade mask (transparent from 86% down)
  - Exported as WebP quality 82
- Result: Clean cutout on dark background, no halo

### og-card.png (113 KB, 1200×630)
- Generated programmatically via Python + PIL
- Dark background (#0b0a14), violet gradient top bar
- Name, title, RightWave, 3-column skill list
- Footer: rohitthakur.in branding

### rw-featured.webp (60 KB)
- Source: Screenshot of RightWave "Humans of RightWave" LinkedIn post (Jun 2025)
- Cropped to 62.5% width to exclude LinkedIn text panel on right
- Resized to 900px wide, WebP quality 85

### rw-spotlight.webp (56 KB)
- Source: Screenshot of RightWave "Employee Spotlight" LinkedIn post (2023)
- Full graphic (clean screenshot provided directly)
- Resized to 900px wide, WebP quality 85

---

## 9. SEO & Schema

**Meta tags (per page):**
```html
<title>Rohit Thakur — Senior Manager IT, Infrastructure & Security | RightWave</title>
<meta name="description" content="...">
<link rel="canonical" href="https://rohitthakur.in/">
```

**Open Graph:** og:type, og:url, og:title, og:description, og:image (og-card.png 1200×630), og:locale (en_IN)

**Twitter card:** summary_large_image

**Schema.org Person (JSON-LD):**
```json
{
  "@type": "Person",
  "name": "Rohit Thakur",
  "alternateName": "Rohit Kumar Thakur",
  "url": "https://rohitthakur.in",
  "jobTitle": "Senior Manager – Server Admin",
  "worksFor": {"@type": "Organization", "name": "RightWave"},
  "address": {"addressLocality": "Noida", "addressRegion": "Uttar Pradesh", "addressCountry": "IN"},
  "sameAs": [LinkedIn, GitHub, both YouTube channels, both Instagrams]
}
```

**sitemap.xml:** Single URL — https://rohitthakur.in/  
**robots.txt:** Allow all, points to sitemap

---

## 10. Security Configuration

### _headers file (Cloudflare Pages)
```
/*
  X-Content-Type-Options: nosniff
  X-Frame-Options: SAMEORIGIN
  Referrer-Policy: strict-origin-when-cross-origin
  Permissions-Policy: camera=(), microphone=(), geolocation=()
  Content-Security-Policy: default-src 'self'; script-src 'self' 'unsafe-inline' 
    https://api.rss2json.com https://api.allorigins.win; 
    style-src 'self' 'unsafe-inline' https://fonts.googleapis.com; 
    font-src 'self' https://fonts.gstatic.com; 
    img-src 'self' data: https://i.ytimg.com https://rohitthakur.in; 
    connect-src 'self' https://api.rss2json.com https://api.allorigins.win https://www.youtube.com; 
    upgrade-insecure-requests

/assets/*
  Cache-Control: public, max-age=31536000, immutable

/*.html
  Cache-Control: public, max-age=0, must-revalidate
```

### Cloudflare dashboard settings
- SSL/TLS: **Full** mode
- TLS version: **1.3** (automatic)
- Always Use HTTPS: **ON**
- Bot Fight Mode: **ON**
- Speed optimizations: **ON**
- HSTS: **Pending** — enable after 1 week of confirmed HTTPS stability

### _redirects file
```
/teaching    /index.html    302
/links       /index.html#connect    302
/projects    /index.html#work    302
```

---

## 11. GitHub Setup

**Account:** github.com/rohitthakurin  
**Site repo:** github.com/rohitthakurin/rohitthakur.in (Public)  
**Profile README repo:** github.com/rohitthakurin/rohitthakurin

**Profile README** covers: role summary, all 6 skill groups, 5 certifications, all social links. Last updated June 2026 — update whenever skills change.

**Git workflow:**
```bash
# Navigate to site folder
cd /Users/rohitthakur/Dropbox/Rohit_Documents/rohitthakur.in

# Make changes to index.html (or other files)

# Push update
git add .
git commit -m "describe what changed"
git push
# Cloudflare auto-deploys in ~60 seconds
```

**Git identity (set once, permanent):**
```bash
git config --global user.name "Rohit Thakur"
git config --global user.email "mail2rohitthakur@gmail.com"
```

**Personal Access Token:** created June 2026, no expiration, `repo` scope only. Used as GitHub password in Terminal. Store securely.

---

## 12. Cloudflare Pages Deploy

**Project name:** rohitthakur-in  
**Preview URL:** https://rohitthakur-in.pages.dev  
**Production URL:** https://rohitthakur.in  
**GitHub repo:** rohitthakurin/rohitthakur.in  
**Branch:** main  
**Framework preset:** None  
**Build command:** (empty)  
**Build output directory:** /  

Every push to `main` triggers automatic deploy. Deploy takes ~30 seconds.

**Custom domains attached:**
- rohitthakur.in → Active, SSL enabled
- www.rohitthakur.in → Active, SSL enabled (redirects to apex)

---

## 13. DNS Configuration

**Registrar:** GoDaddy (all 3 domains)  
**Nameservers (all 3 domains):** gene.ns.cloudflare.com + rob.ns.cloudflare.com

**rohitthakur.in DNS records (managed in Cloudflare):**

| Type | Name | Content | Proxy |
|------|------|---------|-------|
| A | rohitthakur.in | (Cloudflare Pages managed) | Proxied |
| CNAME | www | rohitthakur.in | Proxied |
| TXT | _dmarc | v=DMARC1; p=... | DNS only |

**Pending (indiandalalstreets.in):**
- Add proxied A record (dummy IP 192.0.2.1)
- Create Redirect Rule → 301 to https://www.youtube.com/@VlogsbyRohitThakur

**Pending (thakuracademy.in):**
- Add proxied A record
- Create Redirect Rule → 301 to https://rohitthakur.in

---

## 14. YouTube RSS Video Feed

**How it works:**
1. Page loads → JS fetches both channel RSS feeds via rss2json.com API
2. Parses response → extracts title, video ID, thumbnail URL, watch link
3. Renders 3 cards (UtsavRaag #1, Vlogs #1, UtsavRaag #2)
4. Thumbnails from `i.ytimg.com/vi/{videoId}/hqdefault.jpg`
5. Each card links to `youtube.com/watch?v={videoId}` — opens in new tab
6. Views count on the actual YouTube channel ✅

**RSS feed URLs:**
```
UtsavRaag:        https://www.youtube.com/feeds/videos.xml?channel_id=UCTlbsyz4bFG755aJRcVfzaw
Vlogs:            https://www.youtube.com/feeds/videos.xml?channel_id=UCkOZjHl-LjhCxKeUUMIIuGg
```

**API used:**
```
https://api.rss2json.com/v1/api.json?rss_url={encoded_feed_url}&count=3
```
No API key required. Free tier. Falls back to allorigins.win if rss2json fails.

**Important notes:**
- Does NOT work locally via `file://` — CORS blocks external fetch from local files
- Works perfectly on any HTTPS URL (rohitthakur.in or rohitthakur-in.pages.dev)
- Auto-updates on every page visit — new videos appear automatically, no code change needed
- If you post a new video and want it to appear: just wait, it shows on next visitor's page load

---

## 15. How to Update the Site

### Update any content (text, links, skills)
1. Open `index.html` in any text editor
2. Find the section (search for the text you want to change)
3. Edit, save
4. Push: `git add . && git commit -m "update: what you changed" && git push`
5. Live in ~60 seconds

### Add a new project card
Find the projects section in `index.html`, copy one `<article class="pcard reveal">` block, paste after the last one, update the number, title, description, tags, and link.

### Add a new skill chip
Find the relevant `<div class="schips">` group, add:
```html
<span class="schip">Your new skill</span>
```

### Update your photo
1. Place new photo as `rohit-portrait.webp` in `assets/img/`
2. Push — photo updates automatically

### Add a new YouTube featured video (manual override)
Not needed — videos auto-update from RSS.

### When Teaching launches
1. Replace the "Teaching soon" pill in nav with a real link to `thakuracademy.in`
2. Update the `_redirects` file for `/teaching`
3. Set up `thakuracademy.in` as a separate Cloudflare Pages project

---

## 16. Pending / Future Work

| Item | Priority | Notes |
|------|----------|-------|
| Set up indiandalalstreets.in → YouTube redirect | Medium | Cloudflare Redirect Rule, see §13 |
| Set up thakuracademy.in → rohitthakur.in redirect | Low | Until teaching launches |
| Enable HSTS | Low | Wait 1 week after confirmed HTTPS stability, then enable in Cloudflare SSL/TLS settings |
| Add favicon.ico + apple-touch-icon.png | Low | Currently no favicon — browsers show default |
| Add site.webmanifest | Low | For PWA / home screen add |
| Replace rss2json.com with Cloudflare Pages Function | Optional | Removes third-party dependency, more reliable |
| LinkedIn skills update | Done in session | Add AI/automation skills manually in LinkedIn |
| GitHub profile README update | Done | Update when skills change |
| Real project screenshots in project cards | Optional | Currently gradient placeholders |
| Analytics | Optional | Cloudflare Web Analytics (free, privacy-friendly, no JS needed) |

---

## 17. Key Decisions & Rationale

| Decision | Rationale |
|----------|-----------|
| Single-page over multi-page | Content fits comfortably on one scroll; sparse pages hurt SEO; single file is easier to maintain |
| No % skill bars | Self-assigned numbers carry no credibility with technical audiences; chip groups are honest and extensible |
| No CMS/WordPress | Infrequent updates don't justify a database + PHP runtime + plugin patching surface |
| Cloudflare Pages over Netlify/Vercel | Free, no credit card, global CDN, integrated DNS, and the domain was already pointing there |
| Static LinkedIn card over iframe | LinkedIn embeds show "Page not found" to logged-out visitors; static image works for everyone |
| mailto: over contact form | No backend to maintain or defend; fine for v1; revisit if spam becomes a problem |
| Public GitHub repo | All content is already public via the live site; public repo shows real work on profile |
| Dropbox as working directory | Multi-MacBook workflow; Dropbox syncs files across devices without needing git clone on each machine |
| No trading content on rohitthakur.in | Employer-identity separation and SEBI-adjacency; indiandalalstreets brand kept completely separate |

---

## 18. Social Profiles & Links

| Platform | URL / Handle |
|----------|-------------|
| Website | https://rohitthakur.in |
| LinkedIn | https://www.linkedin.com/in/rohitthakur87 |
| GitHub | https://github.com/rohitthakurin |
| YouTube (devotional) | https://www.youtube.com/@UtsavRaag |
| YouTube (vlogs) | https://www.youtube.com/@VlogsbyRohitThakur |
| Instagram (devotional) | https://www.instagram.com/utsavraag |
| Instagram (vlogs) | https://www.instagram.com/vlogsbyrohitthakur |
| Email | mail2rohitthakur@gmail.com |
| Cloudflare account | Mail2rohitthakur@gmail.com |
| GitHub account | rohitthakurin |

---

*Document created June 2026. Update this file whenever significant changes are made to the site, infrastructure, or skills.*
