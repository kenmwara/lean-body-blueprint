# The Lean Body Blueprint

> $97 fitness funnel for time-poor 9-to-5 workers. "No diet. No gym. No willpower." Three-rule system, instant digital delivery, 5-episode video sequence.

🌐 **Live:** [theleanbodyblueprint.com](https://theleanbodyblueprint.com) *(beta)*
💳 **Price:** $97 USD (one-time, 30-day money-back)
🏗️ **Stack:** Cloudflare Pages + Stripe + Resend + YouTube remarketing
🔒 **Source:** private

---

## What this is

A complete digital fitness product targeting the audience that traditional fitness content underserves — full-time employees who can't fit a gym + meal-prep lifestyle into their workweek. The product is a 3-rule framework ("eat real food," "20-minute bodyweight," "habits over willpower") delivered as a PDF guide + 5 short videos.

Built solo end-to-end: positioning, copy, brand, landing, payment, fulfilment, ad creative.

## The offer

| Field | Detail |
|---|---|
| Price | $97 (one-time, no upsell) |
| Stated value | $161 (struck through on checkout for anchoring) |
| Guarantee | 30-day money-back |
| Delivery | Instant digital download (PDF + bonuses) |
| Hook | No diet. No gym. No willpower. |
| Audience | Full-time 9-to-5 workers, men + women |

## The funnel

```
Facebook / IG ad  →  Landing page (VSL — EP1)
                           │
                           ▼
                  Sales copy + CTA  →  Stripe Checkout ($97)
                           │
                           ▼
                  Thank-you / download page
                           │
                           ▼
                  EP1–EP5 video sequence (YouTube + email)
                           │
                           ▼
                  Events posted to ops.tbot.trade
```

## Architecture

- **Landing + sales:** Cloudflare Pages, deployed via wrangler
- **Payment:** Stripe Payment Link (single price, no upsell — keeps the funnel honest)
- **Fulfilment:** Stripe webhook → Cloudflare Worker → Resend email with download link + bonus PDF list
- **Video hosting:** YouTube (private + unlisted variants for the post-purchase sequence)
- **Remarketing:** YouTube pixel + Meta pixel on landing page, audiences segmented by sequence depth
- **Analytics:** events to `events.tbot.trade/ingest` — lead, checkout-started, purchased, refunded

## Key decisions

### 1. Single price, no order bump, no upsell

Most fitness funnels stack offers. This one doesn't. Cleaner mental model for the buyer, easier to maintain for the operator, and the offer either stands on its own or it doesn't.

### 2. EP1 as the VSL on the landing page itself

The first video in the sequence is the sales video. Buyers and non-buyers get the same opener — buyers continue to EP2-5 via the post-purchase sequence, non-buyers see EP1 and decide. Avoids the "give me your email to watch a video" pattern that's killing modern info-product funnels.

### 3. YouTube for video, not a custom video host

Buyers expect YouTube quality, mobile playback, captions, speed control. Self-hosting (Wistia, Vimeo, Bunny) introduces friction for no gain at this price point. Unlisted videos cover the access-control requirement.

### 4. PDF + bonuses delivered via Worker, not a course platform

Teachable / Kajabi / Thinkific add $50-200/mo and a lot of UI for what is fundamentally "send a download link." A Cloudflare Worker that signs URLs to R2 covers the same use case at $0/month.

## What I'd build next

1. **Customer feedback loop** — short email at day 14 asking about specific results, fed back into landing-page testimonial pool
2. **Affiliate program** — same shape as the other portfolio products
3. **A second tier** — $297 with personal-coaching component for users who finish the 5-episode sequence

## Why this is interesting

It's a complete e-commerce product (paid traffic → landing → checkout → digital delivery → email sequence → support) running on Cloudflare's free tier + Stripe's transaction fees only. **No course platform. No CRM. No analytics SaaS.** Hosting cost: $0/month. Per-transaction cost: Stripe's standard 2.9% + 30¢.

The product is small. The architecture decisions are not — every line of cost is justifiable and every dependency is something I'd defend on a whiteboard.

---

*Source code is private. Architecture and decisions above are the showcase. To discuss, [reach out](https://linkedin.com/in/kenmwara).*
