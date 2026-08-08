# Verification: Store FAQ bot audit

Use this checklist to confirm the Five-check auditor surfaces the correct findings when a stranger runs it against the sample setup.

## Sample setup to verify

**Specimen:** Store FAQ bot that picks an answer from the help center

**Standard:** The answer matches the shopper's real ask — not a nearby FAQ about the same product

**Test sentences (paste these into /play):**

```
how long do i have to return the Nova Buds after they ship
Nova Buds delivery says Friday — can i still cancel
refund for wrong size on the Trail Jacket, not a shipping question
```

## Verification steps

1. **Open /play** and paste the specimen description and the three test sentences above.

2. **Confirm the tool walks all five checks** — it should score each check and surface findings for the FAQ bot setup.

3. **Confirm the deciding check surfaces correctly.** The tool must identify **unowned** as the top crack — the check that decides the call.

4. **Confirm a numeric measurement is demanded.** The tool must not accept vague findings. For the unowned check, it should require a specific count or threshold — for example:
   - How many tickets containing refund/return/cancel words get answered with shipping content?
   - What daily count triggers escalation?

5. **Confirm the call includes an owner on any condition.** The tool should produce a call like:
   > Hold. No part of the system currently treats refund/return/cancel words as a priority signal — ship engineering lead needs to add a dedicated check before Black Friday. Reopen once the three specimen sentences all route correctly with refund words present.

6. **Confirm the tripwire names a number, a danger line, and a watcher.** The tool should produce a tripwire like:
   > Watch the count of tickets containing an explicit refund/return/cancel word that get answered with shipping content. If that exceeds 10 per day during sale week, CX manager escalates to engineering — because that's a fixable, specific miss, not noise.

## Pass criteria

- [ ] All five checks scored
- [ ] Unowned surfaced as the deciding check
- [ ] Numeric measurement demanded for the deciding check (not "keep an eye on it")
- [ ] Call includes owner (engineering lead) and checkable condition (three specimen sentences route correctly)
- [ ] Tripwire includes number (10 per day), danger line (during sale week), and watcher (CX manager)

If any criterion fails, the auditor is not correctly applying the discipline from the builder's specimen.
