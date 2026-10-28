# New page: Property Management in New Haven, CT

**URL slug:** `property-management-new-haven-ct` (this exact slug, because all 5 location pages already link to it).

**Fastest build:** Pages → Service Areas → Hamden → ⋯ → **Duplicate**. Then on the copy:
1. ⚙ Page Settings → General → Navigation title: `New Haven`. URL slug: `property-management-new-haven-ct`.
2. Drag it to the **top** of the Service Areas folder (it's HQ).
3. Replace the text blocks section by section with the copy below. Keep the "Areas We Serve" code block and the "Work with us" layout from the duplicate.
4. Replace the per-page schema (Page Settings → Advanced → Page Header Code Injection) with the block at the bottom of this file.
5. Publish, then **GSC → URL Inspection → Request indexing** for this URL.

---

## SEO fields (⚙ Page Settings → SEO)

**Title Tag:** `Property Management in New Haven, CT` (36 chars + " — MB MGMTS" = 47)

**Meta Description:** `New Haven, CT property management from a downtown office: leasing, tenant screening, maintenance, rent collection and help with local licensing rules.` (150 chars)

---

## Section 1 — Hero

**H1:** Property Management in New Haven, CT

**Intro (Paragraph / Normal text, not a heading):**

New Haven is a renter's city. Most households here rent rather than own, and demand is anchored by employers that don't relocate: Yale University, Yale New Haven Hospital, Southern Connecticut State University and a downtown that keeps adding apartments. For owners, that means steady demand. It also means an older housing stock, a city that actively enforces its housing code, and tenants with a lot of choice.

The typical New Haven investment property is a two- or three-family house: the wood-frame multifamily homes that line streets in Fair Haven, the Hill, Dixwell and Newhallville, alongside the converted Victorians of East Rock and Wooster Square and the more suburban single-family streets of Westville, the Annex and Morris Cove. Tenants range from graduate students and medical residents on academic-year schedules to long-term families and working professionals, and each group needs different leasing, renewal and maintenance timing.

MB Mgmt Services is headquartered at 129 Church St, downtown, so New Haven isn't a market we drive into; it's where we work every day. We manage leasing, screening, rent collection, maintenance and inspections for New Haven landlords and investors, and we keep owners on the right side of the city's rental rules.

---

## Section 2 — Local rules (NEW section; insert after the hero)

**H2:** What's different about renting in New Haven

**Paragraph:**

Owning rental property in New Haven comes with obligations beyond Connecticut state law:

- **Rental licensing and inspections.** The city's Livable City Initiative (LCI) enforces the housing code and runs New Haven's residential rental licensing program, which includes unit inspections. Licenses, inspections and code complaints need someone tracking them.
- **Fair Rent Commission.** New Haven has a Fair Rent Commission where tenants can challenge rent increases they consider excessive. Renewals priced on documented market data hold up; arbitrary increases invite complaints.
- **Lead paint.** Much of New Haven's housing was built before 1978. Federal lead-disclosure rules apply at every lease, and Connecticut and New Haven health authorities enforce lead-hazard requirements, especially in units with young children.
- **Seasonal turnover.** Leases tied to the academic and medical-residency calendar cluster move-outs into a few weeks each summer. Turnover cleaning, repairs and marketing have to be planned months ahead.

---

## Section 3 — Services

**H2:** New Haven Property Management Services

**Paragraph:**
Whether you own a single condo downtown or a portfolio of three-family houses, the work is the same: keep good tenants, keep the building compliant, and keep the money moving. Contact us for a free property audit and we'll show you exactly where your New Haven property stands.

**Our New Haven property management services include:**
- Rental marketing, showings and tenant placement
- Multi-point tenant screening (credit, background, income, landlord references)
- Online rent collection and owner disbursements
- Maintenance coordination with vetted local vendors and 24/7 emergency response
- Move-in, move-out and routine inspections with documented condition reports
- Help keeping rental licensing and city inspections current
- Lease renewals 60–90 days out, with market-based rent adjustments
- Eviction management and Connecticut Housing Court coordination
- Monthly financial reporting and year-end statements

---

## Section 4 — FAQ

**H3:** Frequently Asked Questions — New Haven

**Q: Do I need a license to rent out my property in New Haven?**
A: In many cases, yes. New Haven's residential rental licensing program, run by the Livable City Initiative, covers most non-owner-occupied rental units and includes inspections. Requirements depend on the property, so we confirm what applies to yours during onboarding and help keep your license and inspections current.

**Q: How does the Fair Rent Commission affect rent increases?**
A: Tenants in New Haven can file a complaint with the Fair Rent Commission if they believe an increase is excessive. We price renewals from current market data and document the reasoning, so increases are defensible, and we start the renewal conversation 60–90 days before the lease ends.

**Q: My property was built before 1978. What do I need to know about lead?**
A: Every lease on pre-1978 housing needs the federal lead-based paint disclosure, and lead hazards are taken seriously by state and city health officials, particularly when a child under six lives in the unit. We make sure disclosures go out with every lease and flag lead-related maintenance issues before they turn into orders.

**Q: Where is your office?**
A: Downtown, at 129 Church St, Suite 205, New Haven, CT 06510. Owners are welcome to meet with us in person. Call (203) 903-1241 to set a time.

---

## Section 5 — Areas We Serve
Keep the duplicated code block unchanged. (Its New Haven card now points to this page.)

## Section 6 — Work with us (CTA)

**H2:** Work with us

If you own rental property in New Haven and want to stop managing it yourself, or you're switching from a management company that isn't delivering, MB MGMTS offers a free property audit to show you exactly where you stand and what a professionally managed transition looks like. Call us at (203) 903-1241 or email info@mbmgmts.com.

**Button:** Get a free property audit → `/contact-us`
> The duplicated "Get Started" button has an **empty link** on the live pages. Point it to `/contact-us` here, and on the other 5 pages too.

---

## Per-page schema (⚙ Page Settings → Advanced → Page Header Code Injection)

```html
<script type="application/ld+json">
{
  "@context": "https://schema.org",
  "@type": "Service",
  "name": "Property Management in New Haven, CT",
  "serviceType": "Residential property management",
  "url": "https://www.mbmgmts.com/property-management-new-haven-ct",
  "provider": { "@id": "https://www.mbmgmts.com/#company" },
  "areaServed": { "@type": "City", "name": "New Haven", "containedInPlace": { "@type": "State", "name": "Connecticut" } }
}
</script>
```

---

## ⚠ Greg: verify before publishing

I wrote the market and regulatory context from general knowledge of New Haven, not from MB's records. Please confirm or correct:

1. **Rental licensing scope.** I said the program "covers most non-owner-occupied rental units." Check the current scope with LCI (newhavenct.gov → Livable City Initiative). If you know the exact rule, I'll make it more specific.
2. **Service claims I added:** "help keeping rental licensing and city inspections current" and "flag lead-related maintenance issues." These are reasonable for a full-service manager, but only keep them if MB actually does this.
3. **Neighborhoods** are named only as *market description* (housing types), not as "areas we serve." If you want a "Which New Haven neighborhoods do you manage in?" FAQ like the other pages have, tell me which ones are true.
4. **"Owners are welcome to meet with us in person."** Confirm the Church St office takes walk-ins or appointments.
5. No rent figures are included. If you want a rent-trend line, give me a source (for example your own Buildium data or a recent report) and I'll add it.
