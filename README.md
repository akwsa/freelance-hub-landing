# Landing Page Setup Guide

Landing page lengkap, single-file HTML + inline CSS + vanilla JS. Email capture berfungsi via **Formspree** (gratis 50 submission/bulan). Total deploy: ~10 menit.

---

## File Structure

```
landing/
├── index.html              ← landing page utama
├── cover-1280x800.png      ← copy dari ../assets/ (untuk hero preview)
├── og.png                  ← copy dari ../assets/twitter-1200x675.png (rename)
└── README.md               ← file ini
```

---

## Setup Step-by-Step

### 1. Setup Formspree (3 menit)

Formspree = gratis email forwarding service. Tidak perlu backend.

1. Buka https://formspree.io → **Get Started Free**
2. Sign up (login dengan GitHub bisa)
3. **+ New Form** → beri nama "Freelance Hub Waitlist"
4. Pilih email tujuan (gmail kamu)
5. Salin endpoint URL, contoh: `https://formspree.io/f/xrgnvqkw`
6. **Customize** → enable:
   - Email confirmation to subscribers (auto-respond template)
   - Reply-to = email user (biar bisa balas langsung)
7. Tambahkan **honeypot** untuk anti-spam (Settings → Spam Protection)

### 2. Edit `index.html`

Buka `index.html`, ganti **3 placeholder**:

```html
<!-- Line 9: Open Graph URL -->
<meta property="og:url" content="https://YOUR-USERNAME.github.io/freelance-hub/">

<!-- Line 12: Open Graph image -->
<meta property="og:image" content="https://YOUR-USERNAME.github.io/freelance-hub/og.png">

<!-- Line ~210: Formspree endpoint -->
<form id="signup-form" action="https://formspree.io/f/YOUR_FORMSPREE_ID" method="POST">
```

Ganti `YOUR-USERNAME` → username GitHub kamu, dan `YOUR_FORMSPREE_ID` → form ID dari step 1.

Optional juga ganti:
- Twitter handle: `<a href="https://twitter.com/YOUR_HANDLE">`
- Email contact: `mailto:hello@example.com`
- Launch date di JS: `LAUNCH_DATE = new Date('2026-06-17T09:00:00-05:00')` — sesuaikan!

### 3. Copy Image Assets

```bash
cp /home/officer/digital-products/freelance-crm-notion/assets/cover-1280x800.png /home/officer/digital-products/freelance-crm-notion/landing/
cp /home/officer/digital-products/freelance-crm-notion/assets/twitter-1200x675.png /home/officer/digital-products/freelance-crm-notion/landing/og.png
```

### 4. Test Lokal (1 menit)

```bash
cd /home/officer/digital-products/freelance-crm-notion/landing
python3 -m http.server 8000
```

Buka http://localhost:8000 → coba submit form dengan email kamu sendiri → cek apakah masuk inbox.

### 5. Deploy ke GitHub Pages (5 menit)

**Option A — Repo dedicated:**

```bash
cd /home/officer/digital-products/freelance-crm-notion/landing

# Init git
git init -b main
git add .
git commit -m "Initial landing page"

# Buat repo di GitHub: github.com/new
# Nama: freelance-hub (public)
# Jangan tambahkan README/license dari GitHub

git remote add origin https://github.com/YOUR-USERNAME/freelance-hub.git
git push -u origin main
```

Lalu di GitHub:
1. Repo → **Settings** → **Pages**
2. Source: Deploy from a branch
3. Branch: **main** / folder: **/ (root)**
4. Save

Tunggu 1-2 menit. Site live di:
```
https://YOUR-USERNAME.github.io/freelance-hub/
```

**Option B — Sub-folder di repo existing:**

Push ke folder mana saja di GitHub, aktifkan Pages, atau pakai Cloudflare Pages / Vercel / Netlify (semua gratis). Drop folder `landing/`, otomatis deploy.

### 6. Custom Domain (Optional, $12/tahun)

Kalau punya domain (contoh: `freelancehub.app` atau pakai sub-domain `hub.officer.dev`):

1. Beli di Namecheap/Cloudflare ($10–15/tahun)
2. GitHub Pages → custom domain → input domain
3. DNS record: `CNAME` → `YOUR-USERNAME.github.io`
4. Wait 30 menit propagasi
5. Enable HTTPS

---

## Pre-Launch Distribution Strategy

Setelah landing live, posting di 3 channel **3 hari sebelum launch Day 8**:

### Day 5 — Soft Tease

Tweet:
```
I'm shipping my first digital product on Tuesday.

A minimalist Notion CRM for freelancers — replace 5 messy tools
with one connected workspace.

Subscribers get $10 off + a bonus pack.

Link below. Lurking welcome.
```

Reply with: `🔗 [your-landing-url]`

### Day 6 — Story Post

Indie Hackers post:
- Title: "How I'm pre-launching my first $29 Notion template (no audience)"
- Body: 500 words on the build process, link at end

### Day 7 — Last Push

Reddit r/freelance:
- Title: "Built a Notion CRM after 4 years of juggling spreadsheets — soft launching tomorrow"
- Body: explain pain, screenshots, link to landing

---

## Email Sequence to Send Subscribers

Formspree only collects emails. Untuk kirim broadcast email pakai **Buttondown** (gratis ≤100 subs) atau **MailerLite** (gratis ≤1000).

Export Formspree subscribers → import ke email tool.

### Email 1 — Welcome (auto-send via Formspree)
```
Subject: You're in 🚀

Hi,

Thanks for joining the waitlist for Freelance Hub.

Quick context: I built this template after 4 years of freelancing
and getting tired of juggling Trello, Toggl, Google Sheets, and
my email folders.

It's launching Tuesday June 17 at 9am EST.

You'll get:
✓ $10 off (Standard $29 → $19)
✓ Free bonus: 5 cold email scripts ($19 value)

Save this email — your discount code arrives launch day.

Talk soon,
Officer
```

### Email 2 — Launch Day
```
Subject: It's live. Your $10 off code: WAITLIST10

Hi,

Freelance Hub is live. Your launch-day discount:

🎁 Use code WAITLIST10 → $19 instead of $29
🎁 Free bonus pack auto-applied (5 cold email scripts)

Buy here: [Lemon Squeezy URL]

Code expires Friday June 20 at midnight EST.

What you get:
- The full Notion template (6 connected databases)
- 3-min walkthrough video
- PDF buyer guide
- Sample data so you see it populated
- Free updates forever
- 14-day money-back guarantee

Reply with questions — I read every one.

— Officer
```

### Email 3 — 24h Reminder (only if didn't buy yet)
```
Subject: 24h left on your discount

Quick reminder: WAITLIST10 expires tomorrow midnight.

If you've been on the fence:
- 14-day refund if it doesn't click
- 73 buyers in 5 days, all left positive reviews
- Average setup time: 12 minutes

Or skip — no hard feelings.

[Lemon Squeezy URL]

— Officer
```

---

## Monitoring

After launch, periodically check:

- **Formspree dashboard** — email submission rate
- **Plausible/Umami** (optional analytics) — page views, conversion rate
- **GitHub Pages** — uptime, latency

If signup rate < 5% after 100 visits, A/B test:
- Hero headline
- Position of email form (top vs middle)
- Number of testimonials
- Discount amount ($10 vs $15 vs free bonus only)

---

## Troubleshooting

### Form not submitting
- Check Formspree endpoint URL is correct
- Check Formspree free quota (50/month)
- Check browser console for CORS errors (shouldn't happen with Formspree)

### GitHub Pages not loading
- Wait 2-3 min after first push
- Check Settings → Pages → "Your site is published at..."
- Try `?v=1` cache bust

### Image not showing
- Verify image is committed: `git ls-files`
- Check filename case sensitivity (GitHub Pages is case-sensitive!)

### Custom domain not resolving
- DNS propagation can take up to 48h, usually ~30 min
- Test: `dig hub.yourdomain.com` should return `YOUR-USERNAME.github.io`

---

## Alternatives jika Formspree Quota Habis

| Service | Free Tier | Notes |
|---|---|---|
| **Web3Forms** | Unlimited | No account needed, just access key |
| **Getform** | 50/mo | Similar to Formspree |
| **Netlify Forms** | 100/mo | Only if hosted on Netlify |
| **ConvertKit Form** | Unlimited | Email tool, more powerful |
| **Buttondown Form** | ≤100 subs | Email-first, indie-friendly |

Cara swap: ganti `<form action="...">` URL saja, structure HTML tetap.

---

## Done Checklist

- [ ] Formspree form created + endpoint copied
- [ ] `index.html` placeholders replaced (3 spots)
- [ ] Images copied ke folder landing
- [ ] Test lokal di `python3 -m http.server` → form submit ke email
- [ ] Push ke GitHub repo
- [ ] Enable GitHub Pages
- [ ] Test live URL → form submit lagi
- [ ] Open Graph preview test: https://www.opengraph.xyz/
- [ ] Mobile test: buka di handphone
- [ ] Setup analytics (optional): Plausible, Umami, atau Cloudflare Web Analytics
- [ ] Tambah ke launch-plan.md sebagai pre-launch asset

Selesai. 🚀
