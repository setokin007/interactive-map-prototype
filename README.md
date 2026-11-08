# PCC Interactive Map & Day Planner — Prototype

A clickable prototype of the **"Plan my day"** experience for polynesia.com: an interactive
map of the Polynesian Cultural Center tied to an itinerary builder. Guests explore the
six island villages and evening options, add the moments they want to a day timeline, and
are handed off to the right ticket package.

> **Status:** design prototype, not production code. Schedules, durations, walking times
> and prices are placeholders, and village content is a draft awaiting cultural review.

## What's in it

Two linked pages that share one itinerary:

| File | Page | Purpose |
| --- | --- | --- |
| `design/your-day-and-tickets.dc.html` | 1 · Your day & tickets | Understand the day at the Center, then choose a package |
| `design/plan-my-day.dc.html` | 2 · Plan my day | Map + things to do + the "Your day" timeline; send the day to the app |

Key features of **Plan my day**:

- The gate handout map as the base layer, with a pin for every village, show, venue and
  exhibit, plus zoom and a walking route for the guest's day.
- **Place markers** shared by the map, the timeline and the place cards: each island culture
  has its own colour and two-letter code (SA, AO, TO, FJ, TA, HI); dinner, the HĀ show and
  "around the Center" places have theirs. Type icons mark shows, activities, exhibits, food,
  tours and shopping. Alert colours (red, orange, amber, info navy) are kept for messages only.
- **How long are you staying?** filters the day to the guest's hours, with an overview of
  how the day flows (Marketplace, villages, dinner, HĀ).
- **Things to do** grouped by part of the day, with village panels that inform without
  spoiling ("What to expect", "The rest we'll save for your visit").
- **Your day** — a pinned, scrollable timeline in the right rail with walking times between
  stops, overlap flags, drag-to-reschedule, ticket and coach-pickup summary, and a pinned
  "See packages for this day" bar.
- A section menu on the left that jumps to each section; the eye button hides or shows one.

`design/canvas.json` lays the two pages out on the design canvas. `design/ds/pcc-legacy/tokens.json`
holds the PCC Legacy design tokens the pages were started from.

## How these files run today

The `.dc.html` files are **Design Component** pages from a Claude Design canvas. They are
not plain HTML: each page loads `./support.js`, the canvas runtime that renders the
`<x-dc>` template, the `{{…}}` bindings and the `<sc-if>` / `<sc-for>` blocks. That runtime
is not included here, so opening a file directly in a browser will not render the page.

Images are referenced as `/_blob/<id>`, which only resolves inside the canvas. See
[`assets/README.md`](assets/README.md) for the list of images to export.

## Path to Vercel

To host this as a static site:

1. **Export each page as standalone HTML** from the design canvas (artboard menu → download),
   which bundles the runtime and images, and add the exports under `site/`
   (for example `site/index.html` for Plan my day and `site/tickets.html`).
2. **Bring the images across** into `assets/` if the export doesn't inline them, and
   replace `/_blob/<id>` references with `assets/<file>` paths.
3. **Point Vercel at `site/`** as a static project (no build step). Optional:
   add a `vercel.json` with clean URLs.
4. For production, rebuild the pages as components in the polynesia.com stack
   (Brightspot), using the PRD's recommended map approach: illustrated tiles on
   MapLibre GL JS, with pins, outlines and schedules served from the CMS.

## Before anyone outside the team sees it

- Confirm every presentation time, duration and seating time with Operations.
- Have each village's cultural advisors approve their copy, images and marker colour.
- Replace placeholder prices (`[TOTAL]`, `[PRICE]`) and the sample booking numbers.
- Measure real walking distances from a scaled site plan; current times are estimates.

## Related

- PRD: *PRD — Interactive Map of the Polynesian Cultural Center* (Claude Docs)
- Live prototype: the "PCC Interactive Map — Prototype" design canvas
