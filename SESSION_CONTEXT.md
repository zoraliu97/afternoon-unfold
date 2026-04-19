# Afternoon Unfold — Session Handoff

Paste this into a new Claude session when starting fresh. It gives instant context.

---

## Project
**Afternoon Unfold** — a DIY Craft Blind Box brand by Zora Liu.
Product: personalized mystery craft box curated from customer quiz answers.
Tagline: *"No two alike in the world."*
Brand palette: parchment (`#F5EBE4`), ink (`#1A1208`), rosewood (`#B94F63`), gold (`#C4936A`).
Fonts: Cormorant (serif), Raleway (sans), Great Vibes / Playfair (accents).

## Current file
`/Users/zoraliu/Desktop/web/afternoon-unfold-v14.html` — the live pre-sale version.

Older versions (v13, v12, etc.) are in the same folder — v14 is the one to edit.

## Stripe + payments
- Stripe Business account set up, 5 test Payment Links created (qty 1–5 tiers)
- Receiving bank: TD Bank (currently has login lockout — waitlist for resolve)
- In v14 pre-sale flow, **no Stripe checkout** — just Formspree reservations
- Post-launch (July 4) switches back to Stripe checkout

## Pricing (confirmed: "bump now" strategy)
- Each craft: **$40** in CRAFTS array
- Curation fee: **$15** (CURATION_FEE constant)
- Single craft total: $55 retail
- Bundle discount ladder (applied to craft subtotal before curation fee):
  - 2 crafts: 10% off
  - 3 crafts: 15% off
  - 4 crafts: 20% off
  - 5+ crafts: 25% off
- Pre-sale discount: 15% off retail (`UNFOLD15` code)

## Round 1 / Founding 50 (the pre-sale)
- Cohort name: **"Founding 50"** — only 50 boxes, numbered + signed
- Pre-sale ("Round 1") window: **May 1 – May 10, 2026**
- Soft-open (quiet reservations OK): Apr 19 – Apr 30
- Shipping/launch: **July 4, 2026** (US only)
- Discount code: **`UNFOLD15`** (15% off)
- Reservation flow: no payment, email capture via Formspree → full-page success with box number
- On successful reservation, `PRE_SALE_RESERVED` increments in localStorage (session-level counter)
- `PRE_SALE_RESERVED_BASE` at top of JS is the number Zora manually updates each morning based on Formspree inbox count

## Formspree integration
- Endpoint: `https://formspree.io/f/xaqaoebr`
- Submissions go to: `zoraliu97@gmail.com`
- Three submission types distinguished by `_subject`:
  - `📝 Round 1 Reservation — Box #X — [name]` (full reservation)
  - `📮 Round 1 early-waitlist — [email]` (welcome-popup notify-me)
  - `📮 Waitlist signup — [email]` (modal waitlist for closed/soldout states)

## Zapier auto-send confirmation (being set up)
- Formspree → Gmail auto-reply on new reservation
- HTML email template saved at `/Users/zoraliu/Desktop/web/cards/confirmation-email.html`
- Subject: `You're in ✦ Box #[X] of 50 — Afternoon Unfold Round 1`

## Key code locations in v14
- Pre-sale config constants: search `PRE_SALE_TOTAL` / `PRE_SALE_START` / `PRE_SALE_END`
- CRAFTS array (craft data): search `var CRAFTS = [`
- SCENES object (bundle data): search `var SCENES = {`
- Bundle discount ladder: search `discountPct=0.25`
- Reservation modal: `id="reserve-modal"`
- Welcome popup: `id="welcome-popup"`
- Full-page success: `id="reserved-page"`
- Banner: `id="presale-banner"`

## Git
- Repo: https://github.com/zoraliu97/afternoon-unfold
- Current state: v13 pushed, **v14 NOT pushed yet**
- GitHub Pages serves at: https://zoraliu97.github.io/afternoon-unfold/
- Custom domain purchased: **afternoon-unfold.com** (not yet pointed to GitHub Pages)
- User auth needs fresh PAT or `gh auth login` when pushing

## Card design (the box insert)
- Business card size (3.5" × 2" landscape)
- Design previewed at `/Users/zoraliu/Desktop/web/cards/preview.html`
- Two variants:
  - **Founding 50 card** (for first 50 boxes, 15% off on back)
  - **Regular card** (for post-launch, 10% off on back, "what a bliss to meet you" center script)

## UX/Design decisions locked in
- Italics removed everywhere (use rosewood color for emphasis instead)
- Dark buttons replaced with rosewood gradient pills
- Surprise Me scene removed from quiz Q1 (blind box IS already surprise)
- "It's a gift!" chip on Q1 is part of the main 2×3 grid
- Welcome popup shows 2s after first visit, dismisses for 7 days
- 30s promo modal suppressed during pre-sale window
- Banner hides when any modal is open (overlay-active body class)

## Assets in /assets/
Videos: cover.mp4, unbox.mp4, au-newspaper.mp4, au-newspaper-v2.mp4 (used), palmtree-moves.mp4, wave-survey-bg.mp4
Craft hero images: products/pb-hero.png, ww-hero.png, sy-hero.png, fp-hero.png

## What's still pending
- Push v13/v14 to GitHub (needs auth)
- Point afternoon-unfold.com DNS to GitHub Pages
- Set up Zapier auto-reply (in progress per user)
- Content posting strategy for Instagram/TikTok (discussed 60% mood / 25% product / 10% BTS / 5% tutorials mix)
- Mailchimp/ConvertKit for nurture email sequence May–July
- Card PDFs ready for print (in /cards/ folder)
