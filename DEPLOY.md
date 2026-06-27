# Deploy Guide — rohitthakur.in

Step-by-step instructions to push the site to GitHub and deploy on Cloudflare Pages.

---

## 1. Final file structure

Create this folder on your computer and copy files into it:

```
rohitthakur.in/
├── index.html              ← the main site file (rohit-hub.html renamed)
├── _headers                ← Cloudflare security headers
├── _redirects              ← friendly URL aliases
├── robots.txt
├── sitemap.xml
├── README.md               ← your GitHub profile README (optional here)
└── assets/
    └── img/
        ├── rohit-portrait.webp    ← 26 KB optimised hero photo
        └── rohit-cutout.png       ← full-res transparent cutout (backup)
```

**Important:** rename `rohit-hub.html` → `index.html` before pushing.

---

## 2. Push to GitHub

### First time setup
1. Go to **github.com** → click **+** → **New repository**
2. Repository name: `rohitthakur.in`
3. Visibility: **Public** (required for Cloudflare Pages free tier)
4. Do NOT initialise with README
5. Click **Create repository**

### Push your files
Open Terminal (Mac) or Command Prompt (Windows) and run:

```bash
cd path/to/your/rohitthakur.in/folder

git init
git add .
git commit -m "Initial site launch"
git branch -M main
git remote add origin https://github.com/rohitthakurin/rohitthakur.in.git
git push -u origin main
```

Every future update:
```bash
git add .
git commit -m "describe what you changed"
git push
```
Cloudflare auto-deploys within 60 seconds of every push.

---

## 3. Deploy on Cloudflare Pages

1. Log in to **dash.cloudflare.com**
2. Left sidebar → **Workers & Pages** → **Create** → click the **Pages** tab
3. **Connect to Git** → authorise GitHub → select the `rohitthakurin/rohitthakur.in` repo
4. Build settings:
   - **Framework preset:** None
   - **Build command:** *(leave empty)*
   - **Build output directory:** `/`
5. Click **Save and Deploy**
6. Wait ~30 seconds → Cloudflare gives you a `*.pages.dev` preview URL
7. Open it and verify the site looks correct

---

## 4. Add custom domain — rohitthakur.in

### Step A — Add domain to Cloudflare
1. In Cloudflare dashboard → **Add a Site** → enter `rohitthakur.in` → choose **Free plan**
2. Cloudflare shows you **two nameservers** (e.g. `ada.ns.cloudflare.com`)
3. Log in to your **registrar** (GoDaddy/Namecheap) → find rohitthakur.in → change nameservers to the two Cloudflare ones
4. Wait 5–30 minutes for propagation → Cloudflare zone goes **Active**

### Step B — Attach domain to Pages project
1. Go to your Pages project → **Custom domains** → **Set up a custom domain**
2. Enter `rohitthakur.in` → Cloudflare creates the DNS record automatically
3. Also add `www.rohitthakur.in` as a second custom domain
4. Set up a **Redirect Rule**: www → apex
   - **Workers & Pages** → your project → **Settings** → or use **Rules → Redirect Rules**
   - Match: `www.rohitthakur.in/*` → 301 → `https://rohitthakur.in/$1`

### Step C — SSL & security settings
In Cloudflare dashboard for rohitthakur.in:
- **SSL/TLS** → set to **Full (strict)**
- **SSL/TLS** → **Edge Certificates** → turn **Always Use HTTPS** ON
- **SSL/TLS** → **HSTS** → enable AFTER confirming HTTPS works (sticky — hard to undo)

---

## 5. Redirect domains — indiandalalstreets.in and thakuracademy.in

For each domain, add it as a Cloudflare zone (same nameserver process as above), then:

1. DNS → add a proxied (orange cloud) **A record**: Name `@`, IPv4 `192.0.2.1` (dummy — traffic never reaches it)
2. Also add proxied CNAME: Name `www`, Target `@`
3. **Rules → Redirect Rules** → Create rule:
   - **indiandalalstreets.in**: When hostname = `indiandalalstreets.in` OR `www.indiandalalstreets.in` → 301 → `https://www.youtube.com/@VlogsbyRohitThakur`
   - **thakuracademy.in**: When hostname = `thakuracademy.in` OR `www.thakuracademy.in` → 301 → `https://rohitthakur.in`

---

## 6. Verify everything is working

Run through this checklist after deploy:

- [ ] `https://rohitthakur.in` loads correctly (HTTPS, no warning)
- [ ] `https://www.rohitthakur.in` redirects to apex
- [ ] `http://rohitthakur.in` redirects to HTTPS
- [ ] Photo loads in hero section
- [ ] YouTube video thumbnails load (wait 3–5 seconds)
- [ ] LinkedIn featured post loads
- [ ] All nav links scroll to correct sections
- [ ] LinkedIn, GitHub, Instagram, email links open correctly
- [ ] `https://rohitthakur.in/robots.txt` is accessible
- [ ] `https://rohitthakur.in/sitemap.xml` is accessible
- [ ] Check security headers at **securityheaders.com**
- [ ] Run Lighthouse audit (Chrome DevTools → Lighthouse) — target 90+ all categories
- [ ] `https://indiandalalstreets.in` redirects to YouTube channel
- [ ] `https://thakuracademy.in` redirects to rohitthakur.in

---

## 7. Future updates

**Update site content:**
```bash
# edit index.html, then:
git add .
git commit -m "update: describe change"
git push
# Cloudflare auto-deploys in ~60 seconds
```

**Update video section:** videos auto-refresh on every page visit from YouTube RSS — no action needed when you post new videos.

**Add thakuracademy.in teaching site later:** create a separate Cloudflare Pages project, point the domain to it, and remove the redirect rule.

---

## 8. Auto-renewal reminder

Set a **calendar reminder** 30 days before each domain expiry:
- rohitthakur.in
- indiandalalstreets.in
- thakuracademy.in

Ensure **auto-renew is ON** at your registrar for all three. A lapsed domain — especially `indiandalalstreets.in` — is the real risk.
