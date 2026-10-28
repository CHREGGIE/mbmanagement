# mbmgmts.com — Full Site Audit (2026-10-28)

**Method:** I fetched all 15 URLs (13 pages, `sitemap.xml` and `robots.txt`) with a Googlebot user-agent, parsed the HTML, and rendered key pages in headless Chromium to see what a visitor actually sees. One limit: `app.termly.io` was blocked from my environment, so I couldn't confirm that the Privacy and Terms content loads (see §3).

**Headline:** the handoff's diagnosis holds (no noindex, no robots block, self-referencing canonicals), but the template slop is **much worse than the four-page sample showed.** The worst page is the **homepage**, which still carries most of a real-estate-*agent* demo template. Two of the 10 "not indexed" URLs aren't waiting to be crawled at all: they're **404s**.

---

## 1. Status codes and sitemap

| URL | Status | Note |
|---|---|---|
| `/` | 200 | canonical `https://www.mbmgmts.com` |
| `/rental-property-management` | **404** | gone; no redirect |
| `/pricing` | **404** | gone; its demo content (Sterling, "Former Customer") now lives at `/property-management-services` |
| `/property-management-services` | 200 | **not in the handoff's site map**; it's in the sitemap and the nav |
| `/about-us`, `/contact-us`, `/help`, `/privacy-policy`, `/terms-conditions` | 200 | |
| 5 CT location pages | 200 | |
| `/property-management-new-haven-ct` | **404** | **linked from the "Areas We Serve" block on all 5 location pages** |

- **Sitemap** (`/sitemap.xml`, referenced in robots.txt) lists 12 URLs. That matches the live set, including `/home` (Squarespace's alias for the homepage; its canonical points to `/`, which is fine). Neither 404 is listed. **Open question #5: resolved.**
- **Open question #7: resolved.** `/rental-property-management` returns a real 404. The fix is a 301 (see `paste-ready/01-url-mappings.txt`).
- **robots.txt** is Squarespace's default. It only disallows system paths, and AI crawlers are allowed (good for AI search visibility).

## 2. P1 — Template slop, by page (worst first)

### `/` Home ⚠ worst offender
- **Service cards are real-estate-buyer demo copy:** "We craft a custom roadmap based on your **lifestyle needs, preferred locations**…", "move toward **closing** with confidence". Only three distinct paragraphs, each repeated twice across the six cards (Eviction management, Lease renewal, Leasing, Onboarding, Annual inspection, Off market sale).
- **FAQ answers don't match their questions:** "What is your tenant screening process?" → "**Yes.** Our advisors are experienced in both residential and commercial real estate…". "How do you handle evictions in CT?" → "we provide a detailed invoice…". This sits on the `#frequently-asked-questions` anchor that the nav links to.
- Contact section: "Whether you're exploring your first investment or **preparing to list a cherished family home**…" (realtor demo).
- Typos: H2 "Property **Managements** Services"; "**MG** Mgmts takes the lead".
- No meta description.
- Images are AI demo placeholders (`imgg-gi3-*.png`) plus Unsplash stock.

### `/property-management-services` (this is the old "/pricing" content)
- Every service paragraph is template filler: "We offer a range of solutions designed to meet your needs—whether you're just getting started or scaling something bigger." It's used verbatim for 3 of the 5 services.
- "With **Sterling's** property management…", the placeholder "**Former Customer**" testimonial, and an `imgg-demo-*.png` image.
- No pricing whatsoever, despite having replaced `/pricing`.

### `/contact-us`
- The body is the Squarespace demo intro, verbatim: "**It all begins with an idea.** Maybe you want to launch a business. Maybe you want to turn a hobby into something more…" (53 words, nothing else).

### All 5 location pages
- The bodies are good. Shared 6-word phrases between any two pages come to **4–5%** once nav, footer, "Areas We Serve" and CTA are excluded, well under the 30% rule.
- **But** every page's CTA section still has the demo line "**Driven by curiosity and built on purpose, this is where bold thinking meets thoughtful execution. Let's create something meaningful together.**"
- The "Areas We Serve" New Haven card links to a **404** (above).
- Milford and Bridgeport have **two `<h1>`s** ("Property Management in" / "Milford, CT" split into two heading blocks). Merge each into one block with a line break.
- The intro paragraph on each page is formatted as an `<h3>`. Make it normal paragraph text.
- **Per-page schema is broken** (see §4).

### `/about-us`
- ✅ The stray meta-description H3 from the handoff is **gone**.
- The header image (`20140301_Trade-151_0124-copy.jpg`) is served from a *different* Squarespace site ID, which means it's the template's demo photo.

### Site-wide (header, footer, settings)
- **Footer "About" and "Contact" → `http://squarespace.com`**: confirmed visible on every page.
- **The unconfigured newsletter block is visible to the public** on every page: "This newsletter signup form needs a storage option…". Configure storage or delete the block.
- The footer line "Proudly serving **New haven**, West Haven, **East haven**…" has bad capitalization, and since it's in the footer it shows on every page.
- Settings → Social Links still has the demo accounts: `x.com/squarespace`, `instagram.com/squarespace`, `facebook.com/squarespace`. The icons don't render right now, but the URLs ship in every page's HTML. Delete them.
- Site description (Settings → SEO) is empty.

## 3. Privacy and Terms
Both pages contain only a Termly embed (each with its own policy ID). There is no server-side text, so Google only sees the policy if it renders the JavaScript. I couldn't confirm that the embed loads, because Termly was blocked from my environment. **Check:** in GSC, URL Inspection → *Test live URL* → *View tested page* → Screenshot. Also open both pages in a private window. This matters beyond SEO: `/help` makes SMS/TCPA promises that point to these two pages, and SMS carrier registration (10DLC) checks that they work.

## 4. Structured data (JSON-LD)
- **The site-wide header block has unfilled placeholders:** `logo: /path-to-logo.png`, `image: /path-to-hero.jpg` (both 404), `hasMap: …/place/Your+Business+Address`, `sameAs: …maps?cid=YOUR_GBP_CID`. Its address also drops "Suite 205", and its `areaServed` leaves out Milford and Bridgeport.
- **Per-page blocks were copy-pasted without editing:** Milford and Bridgeport both declare `areaServed: West Haven` (and Bridgeport's `url` is the West Haven URL). East Haven and West Haven point their `url` at `-ct` URLs that 404. All five use `name: "MB MGMTS"` instead of the canonical "MB Mgmt Services".
- Squarespace also emits its own empty `LocalBusiness` (`"address": ""`). Fill in Settings → Business Information (NAP from CLAUDE.md §2) and that block becomes correct instead of contradicting yours.
- Fixes: `paste-ready/02-schema-sitewide.html` and `paste-ready/03-schema-location-pages.html`.

## 5. SEO fields

| Page | Title (as rendered) | Meta description |
|---|---|---|
| Home | New Haven Property Management \| MB MGMTS ✅ | **missing** |
| West Haven | "West Haven — MB MGMTS" ⚠ | **missing** |
| Milford | "Milford — MB MGMTS" ⚠ | **missing** |
| Bridgeport | "Bridgeport — MB MGMTS" ⚠ | **missing** |
| East Haven | ✅ (leading space) | 168 chars, cut off in results |
| Hamden | ✅ (leading space) | 166 chars, cut off in results |
| Services | "Property Management Services — MB MGMTS" | **missing** |
| Help / Privacy / Terms | ok | missing |
| About / Contact | ok | ✅ |

Fixes: `paste-ready/04-seo-fields.md`.

## 6. GSC "Discovered – not indexed" list, re-read

| URL | Real status now |
|---|---|
| `/rental-property-management`, `/pricing` | **404**. They'll move to "Not found". 301 them to `/property-management-services` |
| `/property-management-*` (5) | Good bodies. Fix titles, meta, schema, CTA demo line and broken link, then request indexing |
| `/about-us` | Mostly clean. Swap the demo image |
| `/help` | Real, specific content ✅ |
| `/privacy-policy` | Termly-only. Verify that it renders |

Not on the list but more urgent: **`/`** and **`/property-management-services`**. They're indexed or crawlable *and* they're where most of the slop now sits, and the homepage is the page Google samples most.

---

## Fix order

**Do now (no input needed). All paste-ready:**
1. URL mappings (`01`).
2. Footer About/Contact links → `/about-us`, `/contact-us`.
3. Delete or configure the newsletter block; delete the demo Social Links; fix "New haven"/"East haven" in the footer.
4. Replace the site-wide schema (`02`) and per-page schema (`03`); fill Settings → Business Information.
5. Titles and meta descriptions (`04`).
6. On the 5 location pages: delete the "Driven by curiosity…" line; merge the split H1s (Milford, Bridgeport); turn the H3 intros into paragraphs; point the New Haven card to `/` until a New Haven page exists.
7. Home: fix "Managements" → "Management" and "MG Mgmts" → "MB Mgmts".

**Next. I'll draft these, but each needs input or a decision:**
- **Homepage rewrite** (service cards, FAQ, contact blurb). I can write it from facts already on the site; the fee-inclusion FAQ needs real pricing (open question #3).
- **`/property-management-services` rewrite.** Needs pricing (#3) and testimonials (#4).
- **`/contact-us` copy.** I can write it now from the NAP and the hours listed on `/help`.
- **New Haven location page.** It's HQ, the primary market, already linked from 5 pages, and has no page. It's the highest-value new page, ahead of Brooklyn.
