# Dave Weagle Patent Portfolio

An interactive, single-file HTML reference catalog of US patents and patent applications filed by Dave Weagle — mechanical engineer, co-founder of Evil Bikes, and the most prolific suspension engineer in mountain bike history.

Built and maintained by **[RedFoxRun / PostMillennium MTB](https://postmillennium-mtb.github.io)**.

---

## Live Demo

> **[postmillennium-mtb.github.io/weagle-patents](https://postmillennium-mtb.github.io/weagle-patents)**

---

## What It Covers

| Category | Cards | Notes |
|---|---|---|
| Rear Suspension — DW-Link | 3 | US7048292, US7128329 *(expired 2023)*, US7828314 |
| Rear Suspension — Split Pivot | 2 | US7717212 *(fee expired)*, US8002301 |
| Rear Suspension — DELTA System | 1 | No public standalone patent; placeholder with sourced note |
| Rear Suspension — Orion Dynamics | 1 | Patent numbers TBD; placeholder |
| Front Suspension — Trust Message | 1 | US10549812 (parent) + 11 grouped continuations, toggleable |
| Front Suspension — Specialized Era | 5 | US11524744, US11820457, US11945539, US12258095, US11273887 |
| Design Patents | 8 | D859125 through D880372 (Trust Performance ornamentals) |
| Drivetrain | 3 | APP20220297795/790/793 — sequential adjacent drive; status TBD |
| **Total** | **24 main cards + 11 grouped** | **35 entries; ~53 indexed on Google Patents (see Coverage note)** |

---

## Features

- **Live countdown timers** — every patent with a known expiry shows a running `⏱ 11yr 2mo 14d` badge; auto-switches to `EXPIRED` once the date passes with no manual update needed
- **"Now Public Domain" banner** — calls out the September 2023 expiry of the core DW-Link patent (US7128329) and what that means for manufacturers, with a live "next to expire" list below it
- **Three brand themes** — Ibis (light teal + gold), Pivot (cadet blue + navy + pink), Evil (dark + red); preference saved to localStorage
- **Category tabs** — All Patents / Rear Suspension / Front Suspension / Drivetrain / Design Patents / Timeline
- **Subcategory filter pills** — DW-Link, Split Pivot, DELTA, Orion, Trust/Trvstper, Specialized Era, etc.
- **Clickable status filters** — click the active / expired / pending counters in the stats bar to filter the grid
- **Live search** — searches ID, title, platform, brand, and summary text simultaneously
- **Shareable URLs** — tab, subcategory, status filter, and theme are encoded in the URL hash, so a specific view can be linked directly
- **Timeline tab** — two visualizations:
  - Stacked bar histogram: publications per year by category
  - Gantt chart: patent lifetime bars from publication to expiration, with a "NOW" line; bars are clickable and navigate to the corresponding filtered grid view
- **Trust continuations grouped** — the 11 continuation filings under the Trust Message parent are hidden by default behind a toggleable "Show X related filings" section to reduce clutter
- **Category left borders** — amber (rear), blue (front), teal (drivetrain), lavender (design) on every card, consistent with the timeline color coding
- **Colorblind-safe** — status uses shape + text (● ○ ◆) in addition to color; all accent palettes tested against deuteranopia/protanopia/tritanopia
- **Fully self-contained** — a single `.html` file; no build step, no server, no dependencies beyond Google Fonts

---

## Deploying to GitHub Pages

This is a single HTML file. No build step required.

**First deploy:**

1. Create a repository on GitHub (e.g. `weagle-patents`)
2. Upload `weagle-patents.html` to the repository root via the GitHub web interface (drag and drop or **Add file → Upload files**)
3. In **Settings → Pages**, set Source to `Deploy from a branch`, Branch to `main`, folder to `/ (root)`
4. GitHub will assign a URL like `https://your-username.github.io/weagle-patents/weagle-patents.html`

**To update:**

1. Open the file on GitHub, click the pencil ✏️ icon to edit
2. Make your changes (see **Editing Patent Data** below)
3. Click **Commit changes** — GitHub Pages rebuilds automatically, usually within 60 seconds

> **Tip:** if you want the URL to be cleaner (without `.html`), rename the file to `index.html` and GitHub Pages will serve it at `https://your-username.github.io/weagle-patents/`

---

## Embedding in Pinkbike or Other Sites

The widget is designed for iframe embedding:

```html
<iframe
  src="https://postmillennium-mtb.github.io/weagle-patents/"
  width="100%"
  height="800"
  style="border:none"
  allow="storage-access"
></iframe>
```

**Important iframe caveat:** some iframe hosts (including Pinkbike) sandbox iframes in a way that blocks `localStorage` access. The widget handles this gracefully — if storage is blocked, the theme preference just won't persist between page loads, but everything else works normally. No error or blank page.

If the host requires `allow-same-origin` for storage to work, that attribute needs to be added by the platform, not something this file controls.

---

## Editing Patent Data

All patent records live in a JavaScript array called `PATENTS` near the top of the `<script>` block. Each entry is a plain object. Here is a fully annotated example:

```javascript
{
  // ── IDENTITY ──────────────────────────────────────────────────────────
  id:        "US8002301B2",           // Patent number exactly as on Google Patents
  title:     "Vehicle Suspension Systems for Separated Acceleration Responses",
  subLabel:  "Split Pivot — Concentric Pivot",  // italic sub-heading under title; null to omit
  platform:  "Split Pivot",          // controls the colored platform badge
  category:  "rear",                 // "rear" | "front" | "drivetrain" | "design"
                                     // controls left border color and tab filter
  subcat:    "split-pivot",          // controls subcategory pill filter
                                     // rear: "dw-link" | "split-pivot" | "delta" | "orion"
                                     // front: "trust" | "specialized"
                                     // drivetrain: "drivetrain"
                                     // design: "trust-design"

  // ── DATES ─────────────────────────────────────────────────────────────
  // Countdown and auto-expire only work on dates in the exact format:
  // "Mon DD, YYYY"  e.g. "Mar 11, 2028"
  // Use "TBD" or "~2026" for unknown/approximate dates — no countdown shown
  status:    "active",               // "active" | "expired" | "pending"
                                     // overridden at runtime if expires date has passed
  filed:     "Aug 23, 2007",
  published: "Aug 23, 2011",
  expires:   "Mar 11, 2028",         // countdown badge appears automatically

  // ── ASSIGNMENT ────────────────────────────────────────────────────────
  assignee:  "Split Pivot Inc.",
  brands:    ["Devinci","Salsa","Rocky Mountain","Norco"],  // shown as tag pills

  // ── LINKS ─────────────────────────────────────────────────────────────
  link:         "https://patents.google.com/patent/US8002301B2/en",
  externalLink: "http://www.split-pivot.com/home.html",   // optional second button
  externalLabel:"split-pivot.com",                         // label for the button

  // ── DISPLAY ───────────────────────────────────────────────────────────
  summary:   "One to three sentences describing the patent's key claim...",
  year:      2011,                   // publication year — controls year divider in grid
                                     // and position on the timeline histogram
  highlight: true,                   // true = gold border + accent background (landmark patents)

  // ── OPTIONAL CALLOUT BOXES ────────────────────────────────────────────
  note:      "Expires March 11, 2028. Litigation: ...",
             // amber box with ★ prefix; good for legal / historical context
  asterisk:  "Specific patent numbers to be confirmed.",
             // gray italic box with * prefix; good for data gaps / caveats
}
```

### Adding a new patent

1. Copy an existing entry from the `PATENTS` array that's in the right category
2. Update all fields — at minimum: `id`, `title`, `platform`, `category`, `subcat`, `status`, `filed`, `published`, `expires`, `assignee`, `link`, `summary`, `year`
3. Add it inside the `PATENTS = [ ... ]` array, before the closing `];`
4. Comma-separate entries (each entry ends with `},`)
5. Commit

### Adding a Trust continuation

Trust continuation filings live in a separate array called `TRUST_CHILD_DATA` and appear in the expandable section under US10549812B2 rather than as standalone cards. The structure is simpler:

```javascript
{
  id:        "US10549813B2",
  note:      "Coil spring variant",   // short annotation shown inline; null to omit
  filed:     "Oct 12, 2018",
  published: "Feb 4, 2020",
  expires:   "Aug 28, 2037",
  link:      "https://patents.google.com/patent/US10549813B2/en",
  title:     "Inline Coil Spring Shock"
}
```

### Filling in the DELTA and Orion patent numbers

When specific patent numbers are confirmed, replace the `DELTA-001` and `ORION-001` placeholder entries with real ones. Change:
- `id` to the actual patent number
- `filed`, `published`, `expires` to real dates
- Remove the `asterisk` field (or update it)
- Delete `status:"active"` if unknown and replace with `status:"pending"` if it's an application

---

## Data Accuracy

| Field | Confidence | Source |
|---|---|---|
| Trust patent numbers and dates | High | Directly fetched from Google Patents |
| US8002301B2 expiry (Mar 11, 2028) | High | Confirmed via Justia and Google Patents |
| US7128329B2 expiry (Sep 28, 2023) | High | Confirmed; patent now public domain |
| US7717212B2 "Expired — Fee Related" | High | Confirmed via Justia record |
| DW-Link family continuation expiry dates | Medium | Estimated from 2004 family priority date; continuations expire 20 years from earliest claimed priority, not their own filing date — verify at USPTO Patent Center |
| US11273887B2 dates | Low | Placeholder dates only — verify at USPTO |
| Drivetrain app status (APP2022...) | Low | Status as of September 2022 publication; likely granted, abandoned, or continued by now |
| DELTA patent numbers | Unknown | No standalone patent publicly indexed under this name |
| Orion Dynamics patent numbers | Unknown | Specific numbers not yet confirmed |

### Coverage gap

Google Patents indexes approximately **53 results** for Dave Weagle as inventor. This widget covers **35 entries** (24 main cards + 11 grouped Trust continuations). The gap of ~18 consists primarily of:

- International counterpart filings (EP, CA, AU, WO) for patents already covered here
- Component-industry patents from the e*thirteen era
- Additional continuation and divisional applications within covered families

These are tracked on Google Patents at:
[patents.google.com/?inventor=weagle&q=(dave)&num=100](https://patents.google.com/?q=(dave)&inventor=weagle&num=100&oq=dave+weagle)

---

## Known Issues and To-Do

- [ ] Confirm and replace DELTA placeholder with real patent number(s)
- [ ] Confirm and replace Orion Dynamics placeholder with real patent number(s)
- [ ] Verify current status of three drivetrain applications (APP20220297795/790/793) at USPTO
- [ ] Verify exact adjusted expiry dates for DW-Link continuation US7828314B2 and companion US7048292B2 at USPTO Patent Center
- [ ] Verify US11273887B2 filing, grant, and expiry dates
- [ ] Confirm whether any of the ~18 uncatalogued filings are substantively different from already-covered patents (vs. being international counterparts)
- [ ] Add DW6-specific patent numbers if separately filed (current DW6 callout references the original DW4 family)

---

## Sources

- [Google Patents — Dave Weagle](https://patents.google.com/?q=(dave)&inventor=weagle&num=100)
- [Justia Patents — David Weagle](https://patents.justia.com/inventor/david-weagle)
- [Freehub Magazine — "The Architect"](https://freehub.com/articles/the-architect)
- [BikeRadar — "Four Influential Suspension Designs"](https://www.bikeradar.com/features/tech/four-influential-suspension-designs-named-after-their-creators)
- [Pinkbike — Dave Weagle Patents High-Pivot Drivetrain](https://www.pinkbike.com/news/dave-weagle-patents-high-pivot-drivetrain-system.html)
- [split-pivot.com](http://www.split-pivot.com/home.html)
- [Esker Cycles — Orion Suspension Dynamics](https://eskercycles.com/pages/orionsuspensiondynamics)
- [RMU Mountain Culture — Night Train](https://rmumtnculture.com/products/nighttrain)
- [RMU — Interview with Dave Weagle](https://rmumtnculture.com/blogs/design/interview-with-dave-weagle)
- US Patent and Trademark Office (USPTO) Public Search

---

## Technical Notes

**Single-file architecture** — everything (HTML structure, CSS, JavaScript, patent data) lives in one file with no external dependencies beyond Google Fonts. This means:
- Zero build step
- Works by simply opening the file in a browser
- Entire project fits in one GitHub commit

**Self-expiring status** — the `effectiveStatus()` function checks each patent's `expires` date against `new Date()` at render time. Expired badges and ○ icons appear automatically without any manual updates needed. The countdown timers recalculate on every page load.

**Shareable deep-links** — URL hash encodes tab, subcategory, status filter, and theme:
```
weagle-patents/#tab=rear&sub=split-pivot&status=active&theme=ibis
```
Useful for linking directly to a filtered view in articles or Pinkbike comments.

**Fonts** — Space Mono (patent numbers, data fields), Barlow Condensed (headings, platform badges), Barlow (body text). All loaded from Google Fonts; the widget degrades to system monospace/sans if the CDN is unavailable.

---

## Theme Design

| Button | Inspiration | Background | Primary Accent | Secondary Accent |
|---|---|---|---|---|
| **Ibis** | Ibis Cycles (teal + gold era) | Mint teal `#DCF2EE` | Deep teal `#007868` | Golden yellow `#A87400` |
| **Pivot** | Pivot Cycles (cadet blue) | Cadet blue-gray `#A8B8C8` | Dark navy `#162840` | Pink `#A01850` |
| **Evil** | Evil Bikes (dark + aggressive) | Deep slate `#111520` | Red `#E83838` | Amber `#F0AC28` |

All three themes pass WCAG AA contrast ratios for normal text. Status indicators use shape + text alongside color for colorblind accessibility.

---

## License and Attribution

This catalog is compiled from publicly available USPTO and Google Patents records. Patent text, claims, and drawings are US government works and are in the public domain.

Widget code, design, and editorial content:

```
© RedFoxRun / PostMillennium MTB, 2026
```

You're welcome to fork and adapt this widget for other inventor portfolios or patent catalogs. A credit link back to `postmillennium-mtb.github.io` is appreciated but not required.

**This is not legal advice.** Patent status, ownership, and enforceability should always be independently verified through USPTO or qualified patent counsel before making any commercial or manufacturing decisions.

---

*Compiled June 2026 · Info may contain mistakes · Verify critical details at USPTO.gov*
