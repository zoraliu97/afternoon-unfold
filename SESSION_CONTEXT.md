# Afternoon Unfold — Session Handoff

Paste this at the start of any new Claude session. It gives instant context.

---

## Project
**Afternoon Unfold** — a DIY Craft Blind Box brand by Zora Liu.
Product: personalized mystery craft box curated from customer quiz answers.
Tagline: *"No two alike in the world."*
Brand palette: parchment (`#F5EBE4`), ink (`#1A1208`), rosewood (`#B94F63`), gold (`#C4936A`).
Fonts: Cormorant (serif), Raleway (sans), Great Vibes / Playfair (accents).

## Current file
`/Users/zoraliu/Desktop/web/afternoon-unfold-v15.html` — the live Round 1 pre-sale version (current).
`afternoon-unfold-v14.html` is kept as the previous stable (before the big v15 restructure).

**v15 is the one to edit.** v14 stays frozen as a safety backup.

## Stripe + payments
- Stripe Business account set up, **5 test Payment Links** created (qty 1–5 tiers)
- Receiving bank: **TD Bank** (login access issue — waiting to resolve)
- In v14 pre-sale flow → **no Stripe checkout** — just Formspree reservations
- Post-launch (July 4, 2026) → switches to Stripe checkout with `UNFOLD15` promo code

## Pricing (locked: "bump now" strategy)
- Each craft: **$40** in `CRAFTS` array
- Curation fee: **$15** (`CURATION_FEE` constant)
- **1 craft total: $55 retail / $47 with UNFOLD15**
- Bundle discount ladder (applied to craft subtotal before curation):
  - 2 crafts → 10% off
  - 3 crafts → 15% off
  - 4 crafts → 20% off
  - 5+ crafts → 25% off
- Pre-sale discount: **15% off retail** (`UNFOLD15` code)
- **Free US shipping** baked into retail; US-only audience

## Round 1 / Founding 50 (the pre-sale)
- Cohort name: **"Founding 50"** — only 50 boxes, numbered + hand-signed
- Round 1 window: **May 1 – May 10, 2026**
- Soft-open (quiet reservations accepted): **Apr 19 – Apr 30**
- Shipping/launch date: **July 4, 2026** (US only)
- Discount code: **`UNFOLD15`** (15% off, max 50 redemptions)
- Reservation flow: **no payment now** → email capture via Formspree → full-page success with assigned box number
- Scarcity counter:
  - `PRE_SALE_RESERVED_BASE` at top of JS = Zora manually bumps each morning based on Formspree inbox count
  - Runtime `PRE_SALE_RESERVED` = base + localStorage-persisted session boost (increments after each successful reservation per browser)

## Formspree integration
- Endpoint: `https://formspree.io/f/xaqaoebr`
- Submissions go to: **`zoraliu97@gmail.com`**
- Three submission types distinguished by `_subject` prefix (all plain ASCII — emoji removed to prevent spam filtering):
  - `Founding 50 reservation - Box [N] - [name]` (full reservation)
  - `Round 1 early-waitlist - [email]` (welcome-popup Notify Me signup)
  - `Waitlist signup - [email]` (modal waitlist for closed/soldout states)
- **Spam protection:** honeypot `_gotcha` field on reservation form (bots auto-rejected)
- **Known issue:** Formspree's own spam filter flagged early submissions — cleared by marking as "Not Spam" in Formspree dashboard. Should stay clean now with ASCII subjects + honeypot.

## Confirmation email + Zapier (planned, not live)
- HTML email template saved: `/Users/zoraliu/Desktop/web/cards/confirmation-email.html`
- Subject: `You're in ✦ Box #[X] of 50 — Afternoon Unfold Round 1`
- **Delivery method options:**
  1. Formspree Personal tier upgrade ($10/mo) → built-in autoresponder (simplest)
  2. Zapier Gmail trigger ("New email matching search from noreply@formspree.io") → parse body with Code step → Gmail send action (free tier, 100 tasks/mo)
  3. Manual reply from Gmail for first ~20 reservations (most personal)
- Not yet wired up at time of handoff

## Key code locations in v14
- Pre-sale config constants: search `PRE_SALE_TOTAL` / `PRE_SALE_START` / `PRE_SALE_END` / `LAUNCH_DATE`
- `CRAFTS` array (craft data): search `var CRAFTS = [`
- `SCENES` object (bundle data): search `var SCENES = {` (note: `surprise` entry exists but chip removed from UI)
- Bundle discount ladder: search `discountPct=0.25`
- Reservation modal: `id="reserve-modal"`
- Welcome popup (2s auto-open): `id="welcome-popup"`
- Full-page reservation success: `id="reserved-page"`
- Sticky banner: `id="presale-banner"`
- Formspree endpoint constant: `FORMSPREE_ENDPOINT`
- Honeypot field: `name="_gotcha"` inside reservation form

## Git status (LATEST)
- Repo: **https://github.com/Afternoon-Unfold/afternoon-unfold** (transferred from personal `zoraliu97/…` to the Afternoon-Unfold org)
- Live GitHub Pages URLs (new org):
  - **v15:** https://afternoon-unfold.github.io/afternoon-unfold/afternoon-unfold-v15.html
  - v14 (previous stable): https://afternoon-unfold.github.io/afternoon-unfold/afternoon-unfold-v14.html
- Old personal-owner URLs (`zoraliu97.github.io/…`) are now 404 — update any link that pointed there.
- User auth: classic PAT "Afternoon Unfold Mac 2" (scope `repo`, expires Jul 20 2026) stored in macOS Keychain; pushes are silent, no SSO required on the org.

## Custom domain (IN PROGRESS)
- Domain: **afternoon-unfold.com**
- Registrar: **Cloudflare** (owned by Zora's friend, not Zora's account directly)
- Zora's friend will make the DNS changes — forwarded the exact instructions
- DNS records needed:
  ```
  A      @     185.199.108.153   DNS only (grey cloud)
  A      @     185.199.109.153   DNS only
  A      @     185.199.110.153   DNS only
  A      @     185.199.111.153   DNS only
  CNAME  www   afternoon-unfold.github.io   DNS only
  ```
  Plus SSL/TLS mode set to **"Full"** in Cloudflare
- After DNS propagates:
  - Set custom domain in **https://github.com/Afternoon-Unfold/afternoon-unfold/settings/pages** → `afternoon-unfold.com`
  - Wait for DNS check + SSL provision
  - Enable **Enforce HTTPS**
  - **Rename** `afternoon-unfold-v15.html` → `index.html` so the bare domain loads the pre-sale directly (still needs to happen)

## Card designs (print-ready)
- Business card size **3.5" × 2" landscape**
- HTML previewable at `/Users/zoraliu/Desktop/web/cards/preview.html`
- Print PDFs: `/Users/zoraliu/Desktop/web/cards/card-A.pdf` / `card-B.pdf` / `card-C.pdf`
- Two deliverable variants (unfinalized design choice):
  - **Founding 50 card** — for the first 50 boxes (back: 15% off next order)
  - **Regular card** — for post-launch ongoing orders (back: 10% off next order, center "what a bliss to meet you")
- Plan: handwrite the box number + signature on each of the 50

## UX/Design decisions locked in
- **No italic fonts** — use rosewood color (`#B94F63`) for emphasis instead
- **No dark buttons** — all CTAs are rosewood gradient pills (`linear-gradient(90deg,#8E3A4E,#B94F63)` rounded 999px)
- **No "Surprise me" scene** in quiz Q1 (blind box already contains the surprise factor)
- **"It's a gift!" chip** is part of the main 2×3 grid on Q1 (not stranded alone)
- **Welcome popup** shows 2s after first visit, `localStorage`-dismissed for 7 days
- **30s email promo modal** suppressed during Round 1 window (no double email-capture)
- **Sticky banner** hides when any fullscreen overlay is open (body gets `overlay-active` class)
- **Box # golden badge** — big (140px), wax-seal gold gradient, shown on reservation success
- **Full-page reservation success** (not a pop-up) with "Back to main page" button
- **Flip-digit count-up animation** on welcome popup stats
- **Scroll-responsive floating Instagram + TikTok** icons on right edge

## Assets in /assets/
- Videos used: `cover.mp4`, `unbox.mp4`, `au-newspaper-v2.mp4`, `palmtree-moves.mp4`, `wave-survey-bg.mp4`
- Belief section uses `au-newspaper-v2.mp4` (new attached version, not `au-newspaper.mp4`)
- Craft hero images: `products/pb-hero.png`, `ww-hero.png`, `sy-hero.png`, `fp-hero.png`
- Products gallery: many atmospheric photos in `assets/products/`

## Social handles + hyperlinks (standardized)
- Instagram: `https://www.instagram.com/afternoonunfold` (no dot)
- TikTok: `https://www.tiktok.com/@afternoonunfold` (no dot, capital A in display name)

## Content strategy (discussed, ongoing)
- Brand positioning: **not a DIY tutorial channel** — sells a feeling ("permission to unfold the afternoon")
- Target mix:
  - 60% mood / story / personal narrative
  - 25% product in context (tennis + perler beads, Tokyo mood, etc.)
  - 10% behind-the-scenes (packing, sourcing)
  - 5% actual craft tutorials
- Zora has 9 posts so far (IG + TikTok), none viral — normal for month 0–3
- Content calendar proposed: 12 posts between now and May 1 launch
- Post formats that work: POV crafting, 30-sec timelapses, narrative reels with voiceover, split-screen chaos/calm
- Videos on hand: `tennis_perlerbeads.MOV` (61 sec, good Reel), `tokyo1_moving.MOV` (15 sec, good Story)

## What's still pending after this session
- **Domain DNS** — friend needs to update Cloudflare records
- **Rename v14 → index.html** after domain is live (so bare URL works)
- **GitHub Pages custom domain config** (Settings → Pages → enter `afternoon-unfold.com`)
- **Enforce HTTPS** toggle after SSL cert provisions
- **Auto-reply email** — pick between Formspree paid / Zapier Gmail-trigger / manual
- **Nurture email sequence** (5 emails between May 10 close and July 4 launch) — not written yet
- **Update `PRE_SALE_RESERVED_BASE`** each morning during Round 1 based on Formspree count
- **Resolve TD Bank login** so Stripe payouts work post-launch
- **Content posting** — get first 5 Instagram/TikTok posts live with bio link to GitHub Pages URL
