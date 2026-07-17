# Assets library

Every visual asset used in [index.html](../index.html) and [otp.html](../otp.html), extracted
from each page's inline base64/SVG so they exist as standalone files for reuse (ads, decks,
other pages, handoff).

Both pages are intentionally kept as single self-contained files with everything inlined (see
the perf notes at the top of index.html) — these extracted copies are for reference and reuse
elsewhere, not wired back into the pages.

## Pages

- `index.html` — the marketing landing page
- `otp.html` — the post-signup OTP verification step. On `index.html`, submitting the lead
  form shows a loading state then redirects here (`otp.html`); the email entered is passed via
  `sessionStorage` and shown masked (e.g. `jan***@acme.com`). Verifying the code here redirects
  to `https://dashboard.payglocal.in/app/login`. The 4-digit input, resend countdown, and
  two-panel layout (marketing panel + OTP panel, marketing panel hidden below 900px) are all
  self-contained in that one file.

## logos/

| File | Used as | Source in index.html |
|---|---|---|
| `payglocal-logo-img.png` | Header logo (532x160) | `<a class="logo">` in `#siteHeader` |
| `payglocal-pg-logo-img.png` | Footer logo (532x160) | `.pg-logo` in the footer brand column |

### logos/brands/

Client/partner logos shown in the trust marquee, sourced from the `brands` array in the
page's script (130px tall, cropped/quantized from higher-res source exports):

Air India, Bajaj Allianz, Big Basket, First Cry, GlobalBees, Indigo, Ixigo, Make My Trip,
Myntra, Nalli, Nish Hair, Policy Bazaar, Swiggy.

The marquee itself (`.marquee-wrap`) renders outside of `.wrap` so it scrolls full-bleed
edge-to-edge; only its "Trusted by..." label is wrapped for centered alignment.

## icons/

Small inline UI icons (24x24 unless noted), stroke-based so `stroke="currentColor"` picks up
the surrounding text color:

- `success-checkmark.svg` — 52x52 confirmation check shown after form submit
- `carousel-arrow-left.svg` / `carousel-arrow-right.svg` — shared by both carousels (features + testimonials)
- `feat-international-cards.svg` — "International cards" feature card
- `feat-apple-pay.svg` — "Apple Pay" feature card
- `feat-alternate-payment-methods.svg` — "40+ alternate payment methods" feature card
- `feat-currencies.svg` — "120+ currencies. Settled in INR." feature card
- `feat-fira.svg` — "FIRA on every settlement" feature card
- `feat-fraud-protection.svg` — "Fraud protection built in" feature card

## illustrations/

- `hero-globe.png` (893x888, cropped/quantized from a 1024x1024 source; the source's baked-in
  drop shadow beneath the sphere was stripped via alpha-thresholding, transparency preserved)
  — static globe graphic, spun via CSS in two places and left static in the third:
  - `.hero-bg-globe` — bottom-center behind the hero content, `hero-globe-spin` animation
    (60s/rotation), hidden below the 980px breakpoint
  - `.orb-globe` — center of the "Real outcomes" testimonials showcase, `orb-globe-spin`
    animation (20s/rotation) plus a scroll-triggered zoom-in-then-settle on the wrapper,
    hidden below the 980px breakpoint
  - `.final-cta-bg-globe` — bottom of the closing CTA band, static (no animation)
- `orb-lines.svg` — connector lines in the testimonials "orb" showcase, scroll-triggered to
  draw in one at a time (stroke-dashoffset)
- `feat-int-cards.png`, `feat-apple-pay.png`, `feat-currencies.png`, `feat-fira.png`,
  `feat-fraud-protection.png` (480px wide, cropped/quantized) — bottom-right `.feat-card-decor`
  illustrations for 5 of the 6 feature cards (International cards, Apple Pay, 120+ currencies,
  FIRA, Fraud protection). The 6th card ("40+ alternate payment methods") intentionally has
  none. Apple Pay, FIRA, and Fraud protection use the larger `.feat-card-decor-lg` modifier
  (258px vs 215px).

- `splash-loader.gif` (260x184, 45 frames, ~3s loop, cropped/frame-halved/quantized from a
  552x1200/90-frame/341KB source — a PayGlocal logo build-in-and-fade splash animation) — used
  as the loading indicator in both places: `index.html`'s post-submit loader (`#successView`)
  and `otp.html`'s post-verify loader (`#otpLoading`). Both redirects are timed to ~3.2s so the
  animation plays through before navigating away.

## patterns/

- `takeoff-pattern.svg` — repeating skyline/flight-path pattern used as a CSS
  `background-image` on `.takeoff-pattern` (the "Ready to take off?" CTA band)
