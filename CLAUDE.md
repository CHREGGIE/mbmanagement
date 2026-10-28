# MB Management (mbmgmts.com) — Claude Code Handoff

_Prepared 2026-10-28 for Greg Grinman / Sharpcom. Drop this in the project root (rename to `CLAUDE.md` if you want it auto-loaded). Written to brief a fresh Claude Code session with zero prior context._

---

## 0. Operating model — read first

**Claude Code is a generator here, not a deployer.** mbmgmts.com runs on **Squarespace 7.1**. There is no git repo, no filesystem, and no deploy API for the live site. Claude Code produces copy, code, and schema; **Greg pastes everything into Squarespace by hand.**

Because of that, every deliverable must be **paste-ready and labeled with where it goes:**

- **Page body copy** → markdown, with section headers matching the Squarespace blocks they map to.
- **SEO fields** → labeled `Title Tag:` and `Meta Description:` with character counts, for _Page Settings → SEO_.
- **Schema (JSON-LD)** → a single self-contained `<script type="application/ld+json">` block for _Settings → Advanced → Code Injection_ (per-page header) or a Code Block.
- **CSS / custom code** → labeled for _Code Injection_ (site header) or a per-page Code Block.
- **NAP** → always identical to the canonical block in §2. Never paraphrase it.

Do **not** invent facts to fill a page (pricing numbers, testimonials, neighborhoods served). If a detail isn't in this doc, flag it in §8 and ask Greg.

---

## 1. Engagement goal

Get the 10 "Discovered – currently not indexed" pages indexed and ranking, clean up the template-slop dragging the site's quality signals, and **expand into Brooklyn, NY with one page per neighborhood** (mirroring the existing CT per-city pattern).

---

## 2. Business snapshot + canonical NAP

- **Legal / display name:** MB Management LLC, operating as **MB Mgmt Services** ("MB MGMTS")
- **What they do:** Full-service residential property management for landlords and investors
- **Positioning / voice:** Professional, transparent, proactive; "hassle-free profitability"; local-market-expertise angle. Audience is landlords/investors, not tenants.
- **Platform:** Squarespace 7.1
- **Resident portal:** `mbmgmts.managebuilding.com` (Buildium)

**Canonical NAP — keep byte-identical everywhere (site, schema, GBP, citations):**

```
MB Mgmt Services
129 Church St, Suite 205
New Haven, CT 06510
(203) 903-1241
info@mbmgmts.com
```

**Current service areas (CT):** New Haven (HQ), West Haven, East Haven, Hamden, Milford, Bridgeport.

---

## 3. Current site structure

- `/` — Home (hosts the FAQs anchor `#frequently-asked-questions`)
- **Service Areas** (nav folder) → 5 CT city pages:
  - `/property-management-west-haven`
  - `/property-management-east-haven`
  - `/property-management-hamden-ct`
  - `/property-management-milford-ct`
  - `/property-management-bridgeport-ct`
- `/property-management-services` — services page (holds the old `/pricing` demo content; in nav + sitemap)
- `/rental-property-management` — **404** (verified 2026-10-28; 301 → `/property-management-services`)
- `/pricing` — **404** (verified 2026-10-28; 301 → `/property-management-services`)
- `/property-management-new-haven-ct` — **404, but linked from the "Areas We Serve" block on all 5 location pages**
- `/about-us`
- `/contact-us`
- `/help`
- `/privacy-policy`
- `/terms-conditions`

---

## 4. The indexing problem

GSC reports **10 URLs as "Discovered – currently not indexed."** Full list:

```
/about-us
/help
/pricing
/privacy-policy
/property-management-bridgeport-ct
/property-management-east-haven
/property-management-hamden-ct
/property-management-milford-ct
/property-management-west-haven
/rental-property-management
```

**Diagnosis (from live audit of Bridgeport, West Haven, pricing, about-us):** No technical block is causing this — pages return 200, canonicals are self-referential and correct, no `noindex`, nothing disallowed, location pages are internally linked via nav + cross-link block. "Discovered – not indexed" here means Google has the URLs queued but isn't spending crawl budget. Drivers, in order:

1. **New domain, no external crawl demand** (~70% of it). No real backlink profile, so Google has no urgency signal. Mostly resolved with time + authority signals.
2. **Template-slop failing Google's quality sampling.** Unedited Squarespace demo content (see §5) tells Googlebot the site is low-value, which suppresses crawl appetite site-wide — including for the genuinely good location pages.
3. **Minor completeness gaps** (missing meta descriptions, URL inconsistency).

The location pages themselves are good quality (real, differentiated local content) — they're being held back by the domain's newness and the slop, not by their own merits.

---

## 5. Fix backlog (prioritized)

### P1 — Quality / slop (suppressing crawl appetite)
- **`/pricing` — rewrite fully.** Still carries Squarespace demo leftovers: references "Sterling's property management" and "Westchester's Best Vendors" (wrong company, wrong state), a vendor paragraph duplicated verbatim, "— Former Customer" placeholder testimonials, and demo images named `imgg-demo-*.png`. Needs real pricing + real/omit testimonials (see §8).
- **`/about-us` — clean up.** A stray H3 is actually the meta description pasted in as a heading ("Local market expertise in New Haven, CT to landlords and investors…"). Inconsistent capitalization ("New haven", "East haven"). Newsletter block is unconfigured (shows a "needs a storage option" warning).
- **Audit `/help`, `/privacy-policy`, `/terms-conditions`** for the same template residue before doing anything else to them.

### P1 — Technical
- **Verify `/rental-property-management`.** It returned a **client error (4xx)** on fetch. If it's genuinely 404/403ing for Googlebot, that single page has a trivial explanation (and a different fix) vs. the other nine — confirm its response code first.
- **Fix the footer links.** Footer "About" and "Contact" point to `http://squarespace.com` instead of `/about-us` and `/contact-us` — site-wide. Leaks equity offsite and under-links two core pages.

### P2 — SEO completeness
- **Add meta descriptions** to all location pages (about-us already has one; the city pages don't).
- **Resolve URL inconsistency:** `bridgeport/hamden/milford` carry a `-ct` suffix; `east-haven/west-haven` don't. Pick one convention going forward and 301 any you change. (Lock the convention before building Brooklyn — see §7.)
- **Check title-tag consistency** across all pages.

### P2 — Crawl demand / authority (the real unlock for #1 above)
- Stand up / optimize the **Google Business Profile**.
- Build **local citations** (NAP byte-identical to §2).
- **Request indexing** via URL Inspection for the strong pages first (Bridgeport, West Haven, Hamden), not the thin ones.
- Add **in-body homepage links** to location pages with descriptive anchor text (nav links get discounted).
- **Confirm the sitemap** is submitted and contains exactly the live URL set.

---

## 6. Location-page blueprint (codify to avoid doorway-page slop)

The existing Bridgeport and West Haven pages are the model: each is **genuinely differentiated**, not a city-name swap. Every new location page (CT or Brooklyn) must hold to this, or it risks being treated as a thin doorway page — a real danger once there are 10–20+ near-identical neighborhood pages.

**Required structure per page:**
- **H1:** `Property Management in [Neighborhood/City]`
- **Unique local intro** — neighborhood character, housing stock, typical owner/tenant profile. No shared boilerplate here.
- **Local market context** — rent trends, property types, and any **regulations specific to that locality**.
- **Services** — may be consistent across pages, but framed in local terms.
- **Neighborhood-specific FAQs** — not reused verbatim across pages.
- **"Areas We Serve" cross-link block** — links to sibling location pages.
- **CTA** → contact / resident portal.

**Per-page SEO:**
- Unique `Title Tag` and `Meta Description`.
- `LocalBusiness` (or `RealEstateAgent`) JSON-LD with `areaServed` set to the locality and NAP from §2.

**Hard rules:** only nav/footer/CTA may repeat across pages; everything above must be locally specific; don't ship a page whose body is >~30% shared with a sibling.

---

## 7. Brooklyn expansion plan

**Structure:** one page per neighborhood, same blueprint as §6, under a Brooklyn "Service Areas" parent + a Brooklyn hub page.

**URL convention (proposed):** `/property-management-[neighborhood]-brooklyn` — consistent, borough-scoped. Settle the CT `-ct` inconsistency (§5) and apply one standard to Brooklyn from day one.

**NY ≠ CT — content must change, not just place names:**
- NYC landlord-tenant law, **rent stabilization / rent control**, HPD, and lead/registration rules are entirely different from CT. Generated copy must reflect NYC/Brooklyn regulation, or it'll read as (and be) thin and wrong.

**⚠ The strategic flag — read before generating any Brooklyn pages:** the business NAP is a **New Haven, CT address and a 203 number.** Local/map-pack ranking for "property management in [Brooklyn neighborhood]" strongly favors a local Brooklyn presence (address + local number + a Brooklyn GBP). Without one, the Brooklyn pages are realistically an **organic-only** play, not a map-pack play — and even organic local intent leans on local signals. This needs a decision before the build (see §8).

---

## 8. Open questions — confirm with Greg before generating

1. **Brooklyn NAP:** Is there a Brooklyn address + local (718/347/929) number, or do these run off the New Haven NAP? _(Biggest one — determines whether Brooklyn is a map-pack play or organic-only.)_
2. **Which Brooklyn neighborhoods**, exactly, and in what priority order?
3. **Real pricing numbers** for the `/pricing` rewrite?
4. **Real testimonials** available, or omit until there are?
5. ~~Sitemap~~ — **resolved:** `https://www.mbmgmts.com/sitemap.xml`, 12 URLs, matches the live set.
6. **Brand assets** — logo, brand colors/fonts — if any CSS/code work is in scope.
7. ~~`/rental-property-management` status~~ — **resolved:** 404 (so is `/pricing`).
8. **Social profiles:** do `facebook.com/mbmgmts` / `linkedin.com/company/mbmgmts` exist? (removed from schema until confirmed)
9. **GBP URL** and a real logo/photo URL for schema `sameAs` / `image`.
10. **Homepage "Off market sale" card:** what is the service, or remove it? (`paste-ready/06-homepage.md`)
11. **New Haven page claims:** rental-licensing scope, licensing/lead service claims, in-person meetings, which neighborhoods MB actually manages in (`paste-ready/08-new-haven-page.md`, bottom).
12. **East Haven FAQ lists Short Beach**, which is in Branford. Keep as "nearby" or remove?

---

## 9. What's been verified vs. assumed

- **Full live audit done 2026-10-28** — every page, sitemap and robots.txt: see `audits/2026-10-28-site-audit.md`. Paste-ready fixes are in `paste-ready/`.
- Key corrections to the earlier sample: the **homepage** is the worst slop page (real-estate-agent demo copy, FAQ answers that don't match their questions); `/contact-us` body is Squarespace demo text; every location page has the demo line (under the H1) "Driven by curiosity…"; site-wide and per-page JSON-LD contain placeholders and copy-paste errors; the unconfigured newsletter warning is publicly visible site-wide.
- The `/about-us` stray meta-description H3 is already fixed.
- Location pages also carry wrong-city copy ("Our West Haven… services" on Hamden/Milford; West Haven CTAs on Hamden/Milford/Bridgeport; "Eest Haven"), and the "Get Started" buttons have empty links: see `paste-ready/05`.
- Drafted, awaiting Greg: homepage rewrite (`06`), `/contact-us` copy (`07`), New Haven page (`08`).
- Not verifiable from the sandbox: Termly-embedded content on `/privacy-policy` and `/terms-conditions` (app.termly.io blocked).
- NAP, service areas, positioning, and platform in §2 are taken from the live `/about-us` and `/help` pages.
