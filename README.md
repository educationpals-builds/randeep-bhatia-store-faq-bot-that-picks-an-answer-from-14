# Five-check auditor

Walk any failing setup through five checks, score each, and return a verdict with a tripwire.

---

## Worked example: Store FAQ bot that picks an answer from the help center

**What breaks:** Shoppers get the wrong policy and leave the cart

**Standard:** The answer matches the shopper's real ask — not a nearby FAQ about the same product

---

## Verdict

**Hold.** No part of the system currently treats refund/return/cancel words as a priority signal — ship engineering lead needs to add a dedicated check before Black Friday. Reopen once the three specimen sentences all route correctly with refund words present.

---

## Tripwire

Watch the count of tickets containing an explicit refund/return/cancel word that get answered with shipping content. If that exceeds 10 per day during sale week, CX manager escalates to engineering — because that's a fixable, specific miss, not noise.

---

## Deciding check

**Unowned** — scored 4/5 severity. The system has no owner for refund/return/cancel intent; those words fall through to product-name matching and surface shipping answers instead.

---

## One-paste rebuild block

```
Specimen: Store FAQ bot that picks an answer from the help center
Stakes: Shoppers get the wrong policy and leave the cart
Standard: The answer matches the shopper's real ask — not a nearby FAQ about the same product

Sample failing inputs (from store help-desk chat logs):
1. how long do i have to return the Nova Buds after they ship
2. Nova Buds delivery says Friday — can i still cancel
3. refund for wrong size on the Trail Jacket, not a shipping question

Check scores:
- Unowned: 4
- Copies: 2
- Room: 1
- Stitch: 2
- Ablation: 1

Deciding check: Unowned

Call: Hold. No part of the system currently treats refund/return/cancel words as a priority signal — ship engineering lead needs to add a dedicated check before Black Friday. Reopen once the three specimen sentences all route correctly with refund words present.

Tripwire: Watch the count of tickets containing an explicit refund/return/cancel word that get answered with shipping content. If that exceeds 10 per day during sale week, CX manager escalates to engineering — because that's a fixable, specific miss, not noise.
```

---

## What a stranger gets

Paste your own failing setup — what it does, who gets hurt when it fails, and a few real failing inputs. The auditor walks five checks conversationally, proposes findings with the measurement that would confirm each, and returns a scored audit with a severity story, a call, and a tripwire.

<!-- educationpals-build-verified -->
