# Assets library

Every visual asset used in [index.html](../index.html), [otp.html](../otp.html), and
[dashboard.html](../dashboard.html), extracted from each page's inline base64/SVG so they exist
as standalone files for reuse (ads, decks, other pages, handoff).

All three pages are intentionally kept as single self-contained files with everything inlined
(see the perf notes at the top of index.html) — these extracted copies are for reference and
reuse elsewhere, not wired back into the pages.

## Pages

- `index.html` — the marketing landing page. Submitting the lead form leaves the form (and its
  entered values) exactly as-is and shows a `.fullscreen-loader` overlay (fixed, covers the
  entire viewport, `form-loader.gif`) on top of everything, then redirects to `otp.html`.
- `otp.html` — the post-signup OTP verification step. The email entered on `index.html` is
  passed via `sessionStorage` and shown masked (e.g. `jan***@acme.com`). The 4-digit code is
  checked against a hardcoded dummy value (`9812`); an incorrect code re-shows the entry fields
  with an error instead of proceeding. On success it hides the OTP form and shows an in-column
  loader (`.otp-loading`, contained within the right panel rather than a fullscreen overlay,
  using a smaller 56px `form-loader.gif`) and redirects to `dashboard.html` after ~2.9s. The left
  marketing panel is a single image (`otp-left-panel.png`, `object-fit:cover`) rather than
  hand-built markup; it's hidden below 900px, showing just the OTP panel (4-digit input, resend
  countdown) on mobile.
- `dashboard.html` — a static "Welcome to PayGlocal" onboarding/home screen, built to match a
  reference screenshot of the real post-login dashboard. Dark sidebar nav (Home, Transactions,
  Payment Products, Invoice History), a 4-step onboarding journey (Business details → KYC
  information → Bank verification → Pricing & terms), and a Business Overview section with 4
  metric cards and a Quick Access bar. A `.dash-logout` link in the header (next to the avatar)
  points back to `index.html`. All icons/illustrations are hand-built inline SVG (flat line-icon
  style) rather than pixel-matched to the reference's 3D renders, since only a screenshot (not
  the source graphics) was available. This is the page `otp.html` redirects to after a
  successful OTP.

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
  - `.orb-globe` — center of the "Real outcomes" testimonials showcase, `orb-globe-spin`
    animation (20s/rotation) plus a scroll-triggered zoom-in-then-settle on the wrapper,
    hidden below the 980px breakpoint. This zoom/lines-draw sequence is gated by its own
    IntersectionObserver at `threshold:0.6` (not the generic `threshold:0.12` used for
    `.reveal`), so it only plays once the section is substantially in view — not while it's
    still mostly off-screen.
  - `.final-cta-bg-globe` — bottom of the closing CTA band, static (no animation)
- `hero-globe-blue.png` (893x888, same crop/quantize as `hero-globe.png`) — a hue-shifted copy
  (landmasses rotated from ~228°, an indigo/purple-blue, to ~214°, matching `#0061e3`, via a
  full HSL hue replacement with saturation/lightness preserved per-pixel), used by
  `.hero-bg-globe` (bottom-center behind the hero content, `hero-globe-spin` animation at
  60s/rotation, 0.33 opacity, hidden below the 980px breakpoint). The testimonials and final-CTA
  globes intentionally keep the original `hero-globe.png` hue — only the hero fold was asked
  to shift.
- `hero-globe-animated.gif` (360x355, 20 frames, ~5.9s seamless loop, 64-color palette) — a
  self-rotating alternative rendered from a user-supplied 34MB/1400x1400/176-frame source
  (`Gllobe attempt 5.gif`) by playing the original in headless Chromium and screenshotting 40
  evenly-spaced frames with `omitBackground:true` (direct Pillow frame extraction produced a
  false navy-blue border artifact from a per-frame local-palette decoding bug; browser
  screenshots don't have this problem since they capture already-decoded pixels), then cropping
  to content, downsampling to every other frame, and re-encoding with a shared quantized
  palette. Briefly used in `.hero-bg-globe` in place of `hero-globe-blue.png`, then reverted;
  not currently wired into any page, kept here for reference.
- `orb-lines.svg` — connector lines in the testimonials "orb" showcase, scroll-triggered to
  draw in one at a time (stroke-dashoffset)
- `feat-int-cards.png`, `feat-apple-pay.png`, `feat-currencies.png`, `feat-fira.png`,
  `feat-fraud-protection.png` (480px wide, cropped/quantized) — bottom-right `.feat-card-decor`
  illustrations for 5 of the 6 feature cards. Card order (top row then bottom row): International
  cards, Apple Pay, 120+ currencies / FIRA, Fraud protection, 40+ alternate payment methods — the
  last card intentionally has no illustration. Base size is 215px; Apple Pay uses the smaller
  `.feat-card-decor-md` modifier (232px), 120+ currencies uses the even smaller
  `.feat-card-decor-sm` modifier (201px), and Fraud protection uses the larger
  `.feat-card-decor-lg` modifier (284px). FIRA also starts from `.feat-card-decor-lg` but overrides
  it with an inline `width:256px` (a one-off size only FIRA needs, so it doesn't share a class
  with Fraud protection). `feat-int-cards.png` was re-rendered from its original fanned-card
  source by rotating ~17.5° to level the stack upright (measured via PCA on the image's alpha
  mask, then cropped to content and re-quantized) rather than leaving the original diagonal lean.

- `splash-loader.gif` (260x184, 45 frames, ~3s loop, cropped/frame-halved/quantized from a
  552x1200/90-frame/341KB source — a PayGlocal logo build-in-and-fade splash animation) — no
  longer used by either page (superseded by `form-loader.gif` on both the lead-form and OTP
  loaders, for a consistent loader everywhere); kept here for reference only.
- `form-loader.gif` (90x96, 66 unique frames @ 30ms, ~2s seamless loop, opaque white bg) —
  rendered from `GCC Page loader animation 1.lottie` (a 500x500/96-frame vector Lottie, no
  embedded raster assets) via headless Chromium + lottie-web. Depicts dots scattering, forming
  a curve, then the PayGlocal hexagon logo, looping back to dots — a genuine continuous loop by
  design (verified against live Lottie playback frame-by-frame; the "dots split apart"
  mid-transition is an authentic part of the source animation, not an encoding bug). Used in two
  places, both `.loader-gif-full` but sized differently per context:
  - `index.html`'s `.fullscreen-loader` — a `position:fixed` overlay covering the viewport with
    a translucent/blurred (`backdrop-filter:blur(10px)`) background so the page and the form's
    entered data stay visible (softly) underneath. Displayed at 90px (native resolution, no
    upscale). That submit flow no longer hides the form; it shows the overlay on top and
    redirects after ~2.9s.
  - `otp.html`'s `.otp-loading` — an in-column loader (not an overlay) that replaces the OTP
    form within the right panel only, displayed smaller at 56px to suit the narrower column.
- `otp-left-panel.png` (1100x1244, cropped/quantized from a 1470x1662 source) — the complete
  left-panel marketing visual for `otp.html` (heading, feature bullets, currency card
  illustration, all baked into the image itself), used as-is via `object-fit:cover` rather than
  recreated in HTML/CSS.

## patterns/

- `takeoff-pattern.svg` — repeating skyline/flight-path pattern used as a CSS
  `background-image` on `.takeoff-pattern` (the "Ready to take off?" CTA band)
