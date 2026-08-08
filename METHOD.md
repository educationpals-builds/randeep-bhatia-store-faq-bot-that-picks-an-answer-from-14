# The Five Checks: PRISM

When a setup fails to split work correctly, run these five checks in order. Each letter names a principle; together they reveal whether the system can distinguish what matters.

---

## P — Partition the Space

Does the setup divide the input space into non-overlapping regions?

A store FAQ bot should separate "refund questions" from "shipping questions" from "product questions." If the partitions overlap or leave gaps, inputs land in the wrong bucket or fall through entirely.

**What to measure:** Count how many of your test inputs could legitimately belong to more than one partition. If that number is high, the space isn't partitioned — it's smeared.

---

## R — Run in Parallel

Can multiple checks fire at once, or does the system force a single path?

When a shopper asks "can I still cancel" while mentioning "Nova Buds delivery," the system should be able to detect both a cancellation intent and a delivery reference simultaneously — then decide which matters more.

**What to measure:** For each test input, count how many distinct signals the system can detect before it commits to a single answer. If that count is always one, the system is running serial when it should run parallel.

---

## I — Individuate the Pattern

Does each check have its own detector, or do multiple jobs share one blurry pattern?

A question about returning the Nova Buds and a question about Nova Buds delivery both contain "Nova Buds." If the system latches onto the product name without individuating the action word (return vs. delivery), it collapses distinct intents into one.

**What to measure:** Pick two inputs that share a surface feature but require different answers. Run them both. If they get the same answer, the pattern isn't individuated — it's fused.

---

## S — Stitch the Spectra

When multiple signals fire, does the system combine them with clear priority rules?

"Refund for wrong size on the Trail Jacket, not a shipping question" contains both "Trail Jacket" (product) and "refund" (action) and an explicit negation ("not a shipping question"). The system must stitch these signals together — product identity, action type, explicit negation — and let the action word win.

**What to measure:** Find an input with competing signals. Trace which signal the system weighted highest. If you can't trace it, or if the wrong signal won, the stitching rule is broken or missing.

---

## M — Map What Each Head Sees

Can you inspect what each check detected before the final answer was chosen?

If the FAQ bot returns "Your Nova Buds will arrive Friday" when the shopper asked about a refund, you need to see: Did the system detect "refund"? Did it detect "Nova Buds"? Which one did it act on? Without that map, you're debugging blind.

**What to measure:** For one failing input, list every signal the system detected and the confidence or weight assigned to each. If you can't produce that list, the heads aren't mapped — they're a black box.

---

## The Collapse-to-Monochrome Anti-Pattern

When a system fails multiple PRISM checks, the root cause is often the same: it collapsed a multi-dimensional input into a single feature.

The store FAQ bot saw "Nova Buds" and stopped looking. It didn't partition refund-vs-shipping. It didn't run the action-word check in parallel. It didn't individuate "return" from "delivery." It didn't stitch the product name against the action. It didn't map what it saw.

It went monochrome: one feature, one answer, wrong.

**The fix:** Add a dedicated check for the signal that's being ignored. In this case, the system needs a check that fires on refund/return/cancel words and overrides product-name matching when both are present.

---

## Using PRISM

Walk all five checks for any failing setup. Rate each check (1 = broken, 5 = solid). The lowest-rated check is usually where the fix belongs.

The letters in this file — **P**artition, **R**un, **I**ndividuate, **S**titch, **M**ap — are the framework. Other files in this repository reference "the five checks" without spelling out the acronym.
