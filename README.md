# Human OS — Waitlist Landing Page

The public launch landing page for **Human OS by Vieroots**, with the "HOS Waiting list" form
(viegrow.ai) embedded. Nothing is sold on this page — its single goal is waitlist signups.

## Contents

| File | Purpose |
|---|---|
| `index.html` | The entire page — content, styles and scripts in one self-contained file |
| `og.jpg` | 1200×630 share card for WhatsApp / Instagram / LinkedIn link previews |
| `trigr-home.webp` | Real TRIGR home screen — the hero phone (3D tilt + cursor parallax) |
| `trigr-nutrition.webp` | Real TRIGR nutrition screen — showcase left |
| `trigr-ai.webp` | Real TRIGR AI chat screen — showcase centre |
| `trigr-movement.webp` | Real TRIGR movement screen — showcase right |

**Motion/3D:** hero phone floats, tilts in 3D and follows the cursor (desktop, fine pointers only);
a glare sweep runs across every phone screen; showcase screens fan in 3D toward the centre and
flatten on hover; on mobile the showcase is a swipeable snap carousel. All motion is disabled under
`prefers-reduced-motion`, and everything is CSS transforms — no libraries.

**Design language (v3, dark premium):** deep-ink dark theme (`#05060C`) with indigo/violet gradient
accents, Manrope + Inter, glowing pill buttons, glassy dark cards, drifting gradient orbs, and neon
five-layer colors as the brand thread. Real app screens float free in dark bezels (no background
stages) with glow pools and 3D tilt. Signature moments: the giant gradient HUMAN OS wordmark with
scroll parallax, count-up statistics, a scroll progress bar, and the giant HOS WAITING LIST
typographic close. The form lives in a modal behind the giant CTA (Esc / backdrop / × to close;
opens the form in a new tab if JavaScript is off). No em dashes anywhere in the copy, per the founder.

**Adding more app screens:** resize the capture to 900px wide (webp, quality ~90), drop it in this
folder, and duplicate one `<figure class="shot-fig">` block inside `.shots` in `index.html`
(keep the `width="900" height="1955"` attributes — and never set an image height in CSS without
`height:auto`, that's what caused the stretched-screens bug). A screen whose image file is missing
hides itself automatically (`onerror`), so the page never breaks. Showcase phones render cropped at
the stage's bottom edge by design — the stage height (500px desktop / 460px mobile) controls how
much of the screen shows.

The only external dependencies are Google Fonts (Inter) and the waitlist form embed
(`api.viegrow.ai`). No build step.

## Preview locally

```bash
python3 -m http.server 8146 --directory /Users/user/code/humanos-landing
```

Then open http://localhost:8146.

## Deploy (Netlify, same as the brochure)

Option A — drag & drop: go to https://app.netlify.com/drop and drop this folder.

Option B — CLI:

```bash
npx netlify-cli deploy --dir /Users/user/code/humanos-landing --prod
```

## After choosing the final domain — one required edit

Three tags in `index.html` currently point to the placeholder domain `humanos.vieroots.com`:
`og:image`, `og:url`, and `<link rel="canonical">`. Replace the domain in all three
(OG URLs must be absolute — WhatsApp/Facebook won't load a relative path).
Everything else on the page is domain-independent.

## Launch checklist

- [ ] Update the three placeholder-domain tags (above), redeploy
- [ ] **Trim the waitlist form** in the viegrow builder: it currently has ~12 required fields
      (profession, company, income, best time to reach…). Waitlist best practice is 2–4 fields
      (name, phone, email, city) — every extra required field costs signups. Extra qualification
      can move to a follow-up after signup.
- [ ] Fix in the viegrow form builder: the **Annual Income** field shows the placeholder
      "Company you represent" (copy-paste slip in the form config, not on this page)
- [ ] Submit the form once end-to-end and confirm the entry arrives in viegrow/CRM,
      and that the UTM parameters (the page forwards `?utm_...` into the iframe) land on the lead
- [ ] Add a **Privacy Policy link** in the footer once Vieroots has a policy URL — the page makes
      strong data promises above a data-collection form, and India's DPDP Act expects a notice
- [ ] Optional: add an analytics snippet (even privacy-friendly, e.g. Plausible) to see
      CTA clicks and drop-off per channel
- [ ] Test the link preview: paste the URL into a WhatsApp chat and check the card renders
- [ ] Test the page inside the WhatsApp and Instagram **in-app browsers** on Android and iOS
      (that's where most traffic will open it)
- [ ] Point all four Instagram bios + YouTube description at this URL only when it's live
      (per the launch strategy doc: never before)

## Guardrails baked into the copy (do not undo when editing)

- No claims to predict, prevent, reverse, diagnose or treat disease
- EPLIMO is always "250+ predispositions"
- Member journeys are labelled illustrative, names changed, no photos
- App screens are labelled "Concept interface"
- Dr. Sajeev Nair is "transformational coach, biohacker and author" — never a medical authority
- Face-scan/wearable data are "wellness indicators, not medical measurements"
- "Human OS supports your doctor. It never replaces one."
- No pricing anywhere; no fabricated waitlist counts or fake urgency
