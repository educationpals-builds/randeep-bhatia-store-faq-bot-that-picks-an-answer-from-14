# Audit: Store FAQ bot that picks an answer from the help center

## Specimen under review

**Tool:** Store FAQ bot that picks an answer from the help center

**Stakes if unfixed:** Shoppers get the wrong policy and leave the cart

**Standard for success:** The answer matches the shopper's real ask — not a nearby FAQ about the same product

---

## Real inputs tested

**Input profile:** Short mobile questions with product names in the middle

**Source:** Store help-desk chat logs

### Specimen sentences (verbatim)

1. how long do i have to return the Nova Buds after they ship
2. Nova Buds delivery says Friday — can i still cancel
3. refund for wrong size on the Trail Jacket, not a shipping question

---

## Five-check findings

| Check | Score | Notes |
|-------|-------|-------|
| Unowned | 4 | Critical gap — no component claims refund/return/cancel intent |
| Copies | 2 | Multiple FAQ entries compete without clear winner |
| Room | 1 | Minimal headroom for edge cases |
| Stitch | 2 | Weak handoff between product-name match and intent match |
| Ablation | 1 | Removing product name doesn't improve routing |

---

## Deciding check

**Top crack:** Unowned

The system has no dedicated handler for refund/return/cancel language. When a shopper types "refund for wrong size on the Trail Jacket, not a shipping question," the bot latches onto "Trail Jacket" and returns shipping FAQs — because nothing in the pipeline prioritizes the explicit refund signal over the product-name match.

---

## Call

**Verdict:** Hold

Hold. No part of the system currently treats refund/return/cancel words as a priority signal — ship engineering lead needs to add a dedicated check before Black Friday. Reopen once the three specimen sentences all route correctly with refund words present.

---

## Tripwire

Watch the count of tickets containing an explicit refund/return/cancel word that get answered with shipping content. If that exceeds 10 per day during sale week, CX manager escalates to engineering — because that's a fixable, specific miss, not noise.

---

## Rebuild conditions

- [ ] Engineering lead adds dedicated check for refund/return/cancel words
- [ ] All three specimen sentences route to refund/return policy (not shipping)
- [ ] CX manager confirms monitoring is in place for the tripwire metric
