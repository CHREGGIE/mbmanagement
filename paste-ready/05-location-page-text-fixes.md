# Location pages: copy-paste errors (paste-ready)

**Where:** each page → Edit → the text block named. These are wrong-city errors where the text was copied from West Haven and never updated, plus the demo line under every H1.

| Page | Block | Live text (wrong) | Replace with |
|---|---|---|---|
| **All 5** | Hero, directly under the H1 | "Driven by curiosity and built on purpose, this is where bold thinking meets thoughtful execution. Let's create something meaningful together." | **Delete the block** |
| East Haven | Services list lead-in | "Our **Eest** Haven property management services include:" | "Our East Haven property management services include:" |
| Hamden | Services list lead-in | "Our **West Haven** property management services include:" | "Our Hamden property management services include:" |
| Milford | Services list lead-in | "Our **West Haven** property management services include:" | "Our Milford property management services include:" |
| Hamden | "Work with us" CTA | "If you own rental property in **West Haven** and want to stop managing it yourself…" | "If you own rental property in Hamden and want to stop managing it yourself…" |
| Milford | "Work with us" CTA | same as above | "If you own rental property in Milford and want…" |
| Bridgeport | "Work with us" CTA | same as above | "If you own rental property in Bridgeport and want…" |

## Structure fixes (same pass)
- **Milford, Bridgeport:** the H1 is split across two heading blocks ("Property Management in" / "Milford, CT"). Merge them into one Heading 1 block: `Property Management in Milford, CT` (Shift+Enter for a line break if you want the visual split).
- **All 5:** the first intro paragraph is formatted as Heading 3. Select it and change it to Paragraph (Normal) text.
- **All 5:** in the "Areas We Serve" code block, the New Haven card links to `/property-management-new-haven-ct`. Leave it as is if you publish `08-new-haven-page.md` at that exact URL; otherwise change it to `/`.

## ⚠ Fact check for Greg
- **East Haven FAQ** says "we manage properties throughout East Haven including Foxon, Momauguin, **Short Beach**…". Short Beach is part of **Branford**, not East Haven. Either change it to "and nearby Short Beach" (if you do manage there) or remove it.

## Broken button (all 5 pages)
- The "Get Started" button in the "Work with us" section has an **empty link**. Edit the button → Link → `/contact-us`. Consider renaming it "Get a free property audit".
